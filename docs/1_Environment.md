<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->

# 1. C言語環境構築(Ubuntu gcc)

UbuntuにおいてC言語の環境を作る。

Windowsにおいてgccを使う場合はMinGWやCygwinなどの手段もあるが現在ではWSLという手段があるのでそちらを参考にされたし。WSLに関しては別ドキュメントで説明する。

## インストール

いつも通りaptを使う

```
apt install gcc
```

## コンパイル

サンプルとして以下のコード(sample.c)を用意する。

```C
// sample.c
#include <stdio.h>

int main()
{
	printf("Hello World\r\n");
	return 0;
}

```

Terminalから以下のようにファイルを指定する。
```
gcc -o sample.out sample.c
```
`-o`オプションで出力ファイル名を`sample.out`と指定している。`-o`と指定しない場合はa.outが出力される。

```
./sample.out
```
で実行することができる。

----

[次のセクション "2. makefile" へ](./2_make.md)

----
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
