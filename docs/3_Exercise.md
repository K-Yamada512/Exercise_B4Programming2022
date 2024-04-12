<!--

This document is written in Markdown.
You can preview on such as VisualStudio Code.
If you want to know more, search with "vscode markdown" or refer to official document https://code.visualstudio.com/Docs/languages/markdown .

-->
# 3. 課題

## 提出先
GitHub

パブリックレポジトリかプライベートレポジトリにcollaboratorsに招待してもらう。

## 提出物
- ソースコード
- makefile
- Markdown

1から6の問ごとにレポジトリを作成すること。

Markdownのファイル名は"readme.md"とすること。そこから他のMarkdownファイルの参照をすることは構わない。

`makefile`の代わりに`.sln`,`vcxproj`, `vcxproj.filters`のセットを提出してもよい。

## 提出期限
4月下旬


## 問題

以下の問題は別に画像としても提供する。[image](./3_Exercise_image.md)

### 問1 基本

整数$n$,$m$に対して次の値を計算する関数を作成せよ。コンソールから文字列を読み込む必要はない。関数は外部ヘッダーから読み込むこと。

$$
(1) \ \  \sum_{k=1}^n k^2 \ \ \ (2) \ \  \prod_{k=1}^n \frac{1}{k^2} \ \ \  (3) \ \ n! \ \ \ (4) \ \  {}_n \mathrm{C}_m
$$

Markdownに関数の引数、戻り値、具体的な処理の説明を記述し、出力したコンソールのスクリーンショットを載せること。

### 問2 配列・乱数

1から16までの自然数をシャッフルし、コンソールに列挙するプログラムを作成せよ。
なお、実行するたびに順番は変わる必要がある。

Markdownに関数の引数、戻り値、具体的な処理の説明を記述し、出力したコンソールのスクリーンショットを載せること。

### 問3 構造体

構造体を定義して以下の配列を計算する関数を作成せよ。関数は外部ヘッダーから取り込むこと。

$$
\begin{align*}
{\boldsymbol x} = \left(
		\begin{array}{c}
			5\\
			7
		\end{array}
	\right)
\ \ \ {\boldsymbol y} = \left(
		\begin{array}{c}
			2\\
			3
		\end{array}
	\right)
\ \ \ A = \left(
		\begin{array}{cc}
			1 & 3\\
			4 & 2
		\end{array}
	\right)
\ \ \ B = \left(
		\begin{array}{cc}
			2 & 1\\
			3 & 2
		\end{array}
	\right)
\ \ \ 
\end{align*}
$$

$$
\begin{align*}
(1) \ \ {\boldsymbol x} + {\boldsymbol y}\ \ (2) \ \ {\boldsymbol x} \cdot {\boldsymbol y}\ \ (3) \ \ ^t{\boldsymbol x} {\boldsymbol y}\ \ (4) \ \ A {\boldsymbol x}
(5) \ \ AB\ \ (6) \ \ BA\ \ (7) \ \ B^{-1}\ \ (8) \ \ ^t \left( AB \right)
\end{align*}
$$

Markdownに関数の引数、戻り値、具体的な処理の説明を記述し、出力したコンソールのスクリーンショットを載せること。

### 問4 ファイルの出力・グラフの作成

$y=f(x) = \sin (x)$の$x$の値を区間$[0, 2 \pi]$の範囲でテキストファイルで出力せよ。拡張子は問わない。またそのファイルをgnuplotでレンダリングして、Markdownにスクリーンショットを載せること。

### 問5 数値解析
以下を確かめよ

$$
\begin{align*}
&(1) \ \ \lim_{n \rightarrow \infty} \sum_{m=1}^n \frac{{(-1)}^{m-1}}{m} = \log 2\\
&(2) \ \ \lim_{n \rightarrow \infty} \sum_{m=0}^n \frac{{(-1)}^m}{2m + 1} = \frac{\pi}{4}\\
\end{align*}
$$

Markdownに関数の引数、戻り値、具体的な処理の説明を記述し、出力したコンソールのスクリーンショットを載せること。

### 問6 数値解析

方程式 $x^2 -4 = 0$ を二分法、およびNewton-Rapson法でそれぞれ数値的に解け。

Markdownに関数の引数、戻り値、具体的な処理の説明を記述し、出力したコンソールのスクリーンショットを載せること。

### 問7 数値解析2

以下の落下物体の運動方程式をオイラー法と4次のルンゲ＝クッタ法を用いてそれぞれ解け。  
($`v(t)`$：速度　$`g`$：重力加速度　$`k`$：空気の摩擦の定数　$`m`$：質量)  
ただし$`m=1.0,k=1.0,g=9.8,`$初速$`v(0)=0.0,`$計算終了の時刻$`T_{max}=2.0`$とする。


下の運動方程式にオイラー法と4次のルンゲ＝クッタ法を適用し、各時刻において逐次$`v(t+\Delta t)`$を求めて出力するコードを書く。計算部分は関数を用意する。

$$
\begin{align*}
\frac{d}{dt} v(t) = g - \frac{k}{m}v(t)
\end{align*}
$$

----
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
