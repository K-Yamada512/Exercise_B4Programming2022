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

以下の問題は別に画像としても提供する。[image](./image/pe2022a4.svg)

### 問1 基本

整数$n$,$m$に対して次の値を計算する関数を作成せよ。コンソールから文字列を読み込む必要はない。関数は外部ヘッダーから読み込むこと。
$$
\begin{align*}
&(1) \ \  \sum_{k=1}^n k^2\\
&(2) \ \  \prod \frac{1}{k^2}\\
&(3) \ \  n!\\
&(4) \ \  {}_n \mathrm{C}_m
\end{align*}
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
\bm{x} = \left(
		\begin{array}{c}
			5\\
			7
		\end{array}
	\right)
\ \ \ 
\bm{y} = \left(
		\begin{array}{c}
			2\\
			3
		\end{array}
	\right)
\ \ \ 
A = \left(
		\begin{array}{cc}
			1 & 3\\
			4 & 2
		\end{array}
	\right)
\ \ \ 
B = \left(
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
(1) \ \ \bm{x} + \bm{y} \ \ \ 
(2) \ \ \bm{x} \cdot \bm{y} \ \ \ 
(3) \ \ ^t\bm{x} \bm{y} \ \ \ 
(4) \ \ A \bm{x} \ \ \ 
(5) \ \ AB \ \ \ 
(6) \ \ BA \ \ \ 
(7) \ \ B^{-1} \ \ \ 
(8) \ \ ^t \left( AB \right) \ \ \ 
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


----
[Back to Home](../readme.md)

<!-- Written by Croyfet in 2022-->
