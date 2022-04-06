<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->

# 2. makefile

C言語でソースコードを複数のファイルに分割を始めるとコンパイルのたびに長いコマンドを打つ必要がある、どのように依存しているかわからないため分割コンパイルができない、他人のコードの場合もはや何かわからない、といった状況になる。

例えば

- source.c
- test.c
- test_module.c
- module.h
- module.c
- add.h
- add.c
- sub.h
- sub.c

などというファイルがあった場合どのようにコンパイルすればいいか一つ一つ確認する必要がある。
わかっていても

```
gcc source.cpp module.cpp add.cpp sub.cpp
```

などのコードを打つのは大変である。簡単な例のため、この他に様々なオプションが必要な場合もある。

これらを解決するためにShell Scriptを使う変な人もいるが、

普通は`make`コマンドと`makefile`を使い、ビルド作業を自動化する。

## makeのインストール

いつものapt

```
apt install make
```

ちなみに`gcc`や`make`を一括で入れるときは一つ一つでなく`build-essentials`でも構わない。(余計なものが少し入るが)

## `makefile`を書く

`makefile`自体はただのテキストファイルなのでvimなどで編集するといい。

カレントディレクトリに`makefile`がある状態で

```
make
```

と叩くだけで`makefile`の中身が実行される。

`makefile`は"makefile"で拡張子などはつけてはいけない。"Makefile"というように"M"は大文字でもいい。

makefileの構文は

```makefile
# makefile
_TARGET_ : _DEPENDENT_FILES_
	_COMMAND_
```
のように書き、以上のようなまとまりを`ルール`という。これを複数並べる。

ターゲットを書く順番は関係ない。

しかしデフォルトゴールを指定しない場合は一番最初のターゲットがデフォルトのターゲットとして設定される。

```makefile
# makefile
.DEFAULT_GOAL := _DEFAULT_TAEGET_

_DEFAULT_TARGET_ : _DEPENDENT_FILES_
	_COMMAND_
```

### [makefile sample] simple

ディレクトリ
- sample.c
- makefile

このときsample.cをコンパイルする。sample.cは先ほどのもの。

```makefile
# makefile
sample.out : sample.c
	gcc -o sample.out sample.c
```
これで
```
make
```
とするとgccが実行されてコンパイルできるはずである。

ちなみにコンパイルした後、再び`make`を使うと

```
make: 'sample.out' is up to date.
```

と出るはずである。_TARGET_のファイルが既に存在しているか、_DEPENDENT_FILES_に変更がない場合はmakeはそのターゲットを実行しない。
ちなみに変更を加えればいいわけで、ソースコードを編集したり、`touch`コマンドでタイムスタンプを更新すると
```
touch sample.c
```
`make`は実行されるはずである。

## 引数 ターゲットの指定

ターゲットの指定をmakeの引数とすることができる。

```makefile
# makefile
sample.out : sample.c
	gcc -o sample.out sample.c
test.out : test.c
	gcc -o test.out test.c
```

以上のコードの時デフォルトターゲットであるsample.outは

```
make
```
と`make`コマンドを使用したとき呼ばれるがtest.outは呼ばれない。
sample.outの_DEPENDENT_FILES_にtest.outが書かれているのならtest.outも呼んでくれるのだが、関係のないファイルまでをmakeは呼び出さない。

test.outをコンパイルしたいときは
```
make test.out
```
と指定の_TARGET_を引数に書くことでtest.outのコマンドを実行できる。


## .PHONY
後片付けはするべきである。

よく作成したファイルを削除したい場合がある。`rm`コマンドで削除するのも面倒だし、誤って他の大事なファイルを削除する危険もある。makefileに消したい対象のファイルを書いておきmakeコマンドで削除する。

一般的にはcleanオプションを使い、
```
make clean
```
とする。
しかし上のコマンド、もし"clean"というファイルがあった場合
```
make: 'clean' is up to date.
```
先ほど記した通り`make`はすでにターゲットが存在している場合や、そのターゲットの依存先に変更がない場合、コマンドを実行しない。
同様に"clean"は存在し、依存先が存在しない"clean"ターゲットは実行されないこととなる。

という時のためにダミーターゲット`.PHONY`を使う。

```makefile
.PHONY : _NOT_FILE_TARGET_1_ _NOT_FILE_TARGET_2_
```
スペース区切りで複数書ける。

ここに記述したターゲット名は先ほどの問題を解決する。

### [makefile sample] .PHONY

```makefile
# makefile
.PHONY : clean

sample.out : sample.c
	gcc -o sample.out sample.c

clean :
	rm sample.out
```

ここまでくるともう立派なmakefile

```
make
````
でsample.outを作成、
```
make clean
```
でsample.outを削除できる。

## コマンドの非表示

コマンドを実行するとそのコマンドの内容がコンソールに表示される。

### [makefile sample] visible
```makefile
# makefile
.PHONY : call

call :
	echo "CALLED"
```

```
echo "CALLED"
CALLED
```

コマンドの前に`@`をつけることで非表示にできる。

### [makefile sample] mute

```makefile
# makefile
.PHONY : call

call :
	@echo "CALLED"
```
```
CALLED
```

## 変数
変数の代入には`=`や`:=`など何種類か存在するが基本は`:=`を使う。

代入時にはそのまま変数へ、参照時は`$( )`で変数を囲む。

### [makefile sample] variable

```makefile
# makefile
VAR_TEXT := "CALLED VARIABLE TEXT"
.PHONY : call

call :
	@echo $(VAR_TEXT)
```
```
CALLED VARIABLE TEXT
```

## 定義済み変数
よく使われる変数は定義されている。
makefile内で再代入することで上書きできる。

詳しくは公式ドキュメント [GNU Make Manual](https://www.gnu.org/software/make/manual/html_node/Implicit-Variables.html)

- CC
	- C Compiler
	- デフォルトはCコンパイラーの`cc`
	- `cc`は`gcc`などのシンボリックリンク
- CXX
	- C++ Compiler
	- デフォルトは大抵`g++`
- CFLAGS
	- Cコンパイラーのフラグ
	- Includeオプション `-I`
	- デフォルトは空
- CPPFLAGS
	- Cのプリプロセッサーとプログラムのフラグ
	- デフォルトは空
- CXXFLAGS
	- C++コンパイラーのフラグ
	- Includeオプション `-I`
	- デフォルトは空
- LDLIBS
	- 静的ライブラリ
	- `-l` "-l_LIB_FILES_"
	- デフォルトは空
- LDFLAGS
	- 静的ライブラリのディレクトリ
	- `-L` "-L_DIRECTORY_"
	- デフォルトは空

C言語なら
### [makefile sample] defined variable
```makefile
# makefile
CC := gcc
CFLAGS := -o sample.out
CPPFLAGS := 
LDFLAGS := 
LDLIBS := 

sample.out : sample.c
	$(CC) $(CFLAGS) $(CPPFLAGS) $(LDFLAGS) $(LDLIBS) sample.c
```
などのように書いておくとよい。
"定義済み"であるのだからCCは定義する必要はないが誤って別のCコンパイラが呼ばれる対策にはなる。他のフラグはどうせデフォルトでは空なので再定義しても大した問題はない。

## 自動変数

ターゲットファイルは完成するファイル名なのだからコマンドにも同じファイル名を書くことになる。

`$@`は"そのターゲット名"を指す。他にも`$`+"記号"な自動変数は存在するが可読性を考えるとこれぐらいだろう。

### [makefile sample] auto variable

```makefile
# makefile
sample.out : sample.c
	gcc -o $@ sample.c
	@echo "exported as \""$@"\""
```
```
gcc -o sample.out sample.c
exported as "sample.out"
```


## 改行
バックスラッシュで改行

下記の例だとあまり恩恵は感じないがファイル名が長いと重宝。

### [makefile sample] break
```makefile
# makefile
sample.out : \
		sample.c\
		add.c\
		sub.c
	gcc -o sample.out sample.c
```

## マナー

行儀よく以下ぐらいは書いておくと良いだろう。

少なくとも`clean`は欲しい。
`rm -f`のオプションはもし存在しない場合エラーを出すのを避けるため。

cleanの他には"install"で完成したものを指定のディレクトリに移動させたりするなどもある。

### [makefile sample] manners
```makefile
# makefile
.PHONY : clean help

CC := gcc
CFLAGS := -o sample.out
CPPFLAGS :=
LDFLAGS :=
LDLIBS :=

sample.out : sample.c
	$(CC) $(CFLAGS) $(CPPFLAGS) $(LDFLAGS) $(LDLIBS) sample.c

clean :
	rm -f sample.out

help :
	@echo "option"
	@echo "(default) : compile"
	@echo "    clean : Remove files"
	@echo "     help : this"
```


----

[次のセクション "3. 課題" へ](./3_Exercise.md)

----
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
