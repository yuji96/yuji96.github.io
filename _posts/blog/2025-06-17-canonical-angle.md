---
categories:
  - blog
date: 2025-06-17 00:00:00 +0900
math: true
tags:
  - math
title: メモ：正準角と特異値分解の関係
parse_block_html: true
published: true
---

$$
\newcommand{\t}{\mathsf{T}}
\newcommand{\bm}[1]{\boldsymbol{#1}}
$$

## 目的
$d$ 次元空間 $\mathbb{R}^d$ の部分空間 $\mathcal{P, Q}$ における正準角がなぜ特異値分解で求められるのかを知りたい．
（YANS2024 でそういう話を聞いたことがきっかけで書いた記事）

## 定義
$d$ 次元空間 $\mathbb{R}^d$ の $m$ 次元部分空間 $\mathcal{A}$ の正規直交基底を $\\{\bm{a}_1,...,\bm{a}_m \\}$ とする．
同様に，$n$ 次元部分空間 $\mathcal{B}$ の正規直交基底を $\\{ \bm{b}_1,...,\bm{b}_n \\}$ とする．
<!-- % すなわち，$\mathcal{P} = \langle \psi_1,...,\psi_m \rangle, \mathcal{Q} = \langle \varphi_1,...,\varphi_m \rangle$. -->
また，各正規直交基底を並べた行列をそれぞれ
<!-- % 各部分空間$\mathcal{A, B}$の基底を並べた行列をそれぞれ -->
$\bm{A}=[\bm{a}_1,...,\bm{a}_m]~\in~\mathbb{R}^{d\times m},$
$\bm{B}=[\bm{b}_1,...,\bm{b}_n] \in\mathbb{R}^{d\times n}$ とおく．
さらに，$d$ 次元空間 $\mathbb{R}^d$ から部分空間 $\mathcal{A, B}$ への射影行列をそれぞれ $\bm{P}, \bm{Q}\in\mathbb{R}^{d\times d}$ とおく．


## 補題１：射影行列の準備
<!-- %$d$次元空間 $\mathbb{R}^d$から -->
$m$ 次元部分空間 $\mathcal{A} = \langle \bm{a}_1,...,\bm{a}_m \rangle$ への射影行列 $\bm{P}\in\mathbb{R}^{d\times d}$ は，$\bm{P} = \bm{AA}^\t$ である．

（プチ証明）
まず，任意の $\bm{x}\in\mathbb{R}^d$ について，$\bm{Px} \in\mathcal{A}$ となることを確認する．
$\bm{Px}$ を計算すると，

$$
\begin{align}
    \bm{Px} = \bm{A}\bm{A}^\t \bm{x} = (\bm{a}_1^\t \bm{x}) \bm{a}_1 + \cdots + (\bm{a}_n^\t \bm{x}) \bm{a}_n
\end{align}
$$

となり，$\mathcal{A}$ の基底の線形結合で表現できているから $\bm{Px} \in\mathcal{A}$ である．

次に，$\bm{P}$ が射影行列であることの必要十分条件である，$\bm{P}^2=\bm{P}$ を満たすことを確認する．
行列 $\bm{A}$ の各列は直交より，$\bm{A}^\t\bm{A} = \bm{I}_m$ であるから，

$$
\begin{align}
    \bm{P}^2 = (\bm{AA}^\t)(\bm{AA}^\t) % &= \bm{A}(\bm{A}^\t\bm{A})\bm{A}^\t \\
    = \bm{A} (\bm{A}^\t \bm{A}) \bm{A}^\t
    = \bm{AA}^\t %\hspace{3em}      % (\because \bm{A}^\t\bm{A} = \bm{I}_m) \\
    = \bm{P}.
\end{align}
$$


## 補題２：$\bm{PQ}$ の固有ベクトルは $\mathcal{A}$ 上にある
行列 $\bm{PQ}$ の任意の固有ベクトル $\bm{x}$ をとる．
このとき，$\bm{PQx} = \lambda \bm{x}$ が成り立つ．
左辺は $\bm{P}$ で射影されているから $\bm{PQx}\in\mathcal{A}$ より，右辺でも $\bm{x}\in\mathcal{A}$ が成り立つ．


## 本題（一歩手前）：正準角と固有値の関係
射影行列の積 $\bm{PQ}\in\mathbb{R}^{d\times d}$ のある固有値を $\lambda$ としたとき，
正準角 $\theta$ について，$\lambda = \cos^2\theta$ が成り立つ．

<br>

$\bm{PQ}$ の任意の固有ベクトル $\bm{a}\in\mathcal{A}$ をとる（補題２）．
このとき，$\bm{PQa}=\lambda\bm{a}$ であるから，以下が成り立つ．

$$
\begin{align}
    \lambda = \frac{\| \bm{PQa} \|}{\| \bm{a} \|}
    = \frac{\| \bm{PQa} \|}{\| \bm{Qa} \|} \cdot \frac{\| \bm{Qa} \|}{\| \bm{a} \|}
    % = \frac{\| \bm{Pb} \|}{\| \bm{b} \|} \cdot \frac{\| \bm{Qa} \|}{\| \bm{a} \|}.
\end{align}
$$

まず，$\dfrac{\\| \bm{Qa} \\|}{\\| \bm{a} \\|}$ について考える．
$\bm{a}$ を $\mathcal{B}$ 上にある $\bm{b}$ に射影すると，射影の定義より，

$$
\begin{align}
    \bm{Qa} = \dfrac{\bm{a}^\t \bm{b}}{\| \bm{b} \|^2} \bm{b}
\end{align}
$$

となる．したがって，両辺のノルムをとり $\\| \bm{a} \\|$ で割ると，

$$
\begin{align}
    \dfrac{\|\bm{Qa}\|}{\|\bm{a}\|} = \dfrac{\bm{a}^\t \bm{b}}{ \|\bm{a}\| \| \bm{b} \|} 
    = \cos\theta
\end{align}
$$

が成り立つ．

次に，$\dfrac{\\| \bm{PQa} \\|}{\\| \bm{Qa} \\|}$ について考える．
$\bm{a}$ は $\bm{PQ}$ の固有ベクトルだったから，$\bm{Qa}$ は $\bm{P}$ により $\bm{a}$ 上に射影される．
すなわち，
<!-- % \begin{align}
%     \bm{Pb} = \dfrac{\bm{b}^\t \bm{a}}{\\| \bm{a} \\|^2} \bm{a}
% \end{align} -->
$\bm{P(Qa)} = \dfrac{(\bm{Qa})^\t \bm{a}}{\\| \bm{a} \\|^2} \bm{a}$
が成り立つから，同様にして，
<!-- % \begin{align}
%     \dfrac{\\|\bm{Pb}\\|}{\\|\bm{b}\\|} = \cos\theta
% \end{align} -->
$\dfrac{\\|\bm{PQa}\\|}{\\|\bm{Qa}\\|} = \cos\theta$
が成り立つ．
以上より，$\lambda = \cos^2\theta$ が示せた．

<br>

上記の証明において，固有値 $\lambda$ を最大固有値とすれば，
$\cos^2\theta$ が最大，すなわち，最小の正準角 $\theta$ が得られる．

## 本題：正準角のコサインの求め方

上の証明より，$\bm{PQ}=\bm{A}\bm{A}^\t \bm{B}\bm{B}^\t$ の固有値の平方根を求めれば良いのだが，$\bm{PQ}$ は $d\times d$ 行列であるため計算量が大きい．
<!-- % しかしPQのサイズはddであり，興味があるのは部分空間だけなのに計算オーダーはd次元になってしまう． -->
そこで，$\bm{A}\bm{A}^\t \bm{B}\bm{B}^\t$ の固有値が $\bm{B}^\t\bm{A}\bm{A}^\t \bm{B}$ の固有値と等しいというテクを使う．

任意の固有ベクトルについて $\bm{A}\bm{A}^\t \bm{B}\bm{B}^\t \bm{x}=\mu \bm{x}$ が成り立つとき，
両辺に $\bm{B}^\t$ を掛けると \\
$\bm{B}^\t\bm{A}\bm{A}^\t \bm{B} (\bm{B}^\t \bm{x}) =\mu (\bm{B}^\t \bm{x})$ も成り立つ．
これは固有ベクトルが $\bm{B}^\t \bm{x}$ であり，固有値は $\bm{B}^\t$ を掛ける前と変わらないことを意味する．

こうすると，嬉しい点が2つある．
まず，行列サイズが $n\times n$ に落ちる．
さらに $(\bm{A}^\t \bm{B})^\t (\bm{A}^\t \bm{B})$ の形になった．
これにより $\bm{PQ}$ を計算して固有値分解をするのではなく，$\bm{A}^\t \bm{B}$ だけ計算して特異値分解を適用すれば正準角のコサインが求められる．

まあ，今回のケースだと固有値分解と特異値計算の計算量は大して変わらないんだけど．
コードはスッキリする．
最大固有値だけが欲しいなら，固有値をべき乗法で計算したほうがむしろ速そうだが，
それを自分で実装するよりも numpy の関数で svd を計算するのがベストだと思う．

