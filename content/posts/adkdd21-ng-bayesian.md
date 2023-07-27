---
title: "Bayesian Time Varying Coefficient Model with Applications to Marketing Mix Modeling"
date: 2023-07-07T10:20:22+09:00
draft: false
tags: ["AdKDD", "AdKDD 2021", "論文", "TODO", "Bayesian", "時系列モデリング", "統計モデリング", "Marketing Mix Modeling", "状態空間モデル"]
---

- 学会: AdKDD 2021
- http://papers.adkdd.org/2021/papers/adkdd21-ng-bayesian.pdf


## TODO

時系列モデリングや統計モデリングに関する知識が不足しているので、勉強してからよみなおす

## 内容

Marketing Mix Modelingはマーケティング費用を投資する際に、リターンを理解し、投資の分配方法を最適化するためのツール

### 問題設定

限界収益が逓減する支出変数の関数として売上を表現することは、アトリビューションモデルやマーケティングレスポンスモデルの基本的な特性のひとつである。
この視点から、以下のように乗法的関数としてモデル化する。
$$
\hat{y_t} = g(t)\cdot\Pi_{p=1}^P f_{t,p}(x_{t,p}), t=1,2,\dots,T
$$
ここで、 $x_{t,p}$ は説明変数、 $\hat{y_t}$はマーケティングの応答変数、 $g(t)$ は時系列の過程であり、 $f_{t,p}(x_{t,p})$ は $p$ 番目のコストカーブ関数である。Pは説明変数の数で、Tは時系列の長さである。

たとえば、 $g(t)$ でトレンドと季節性を表し、 $f_{t,p}(x_{t,p})$ はチャンネルごとの時間変化するコストカーブ関数を表す。

logをとれば状態空間モデルとなるが、MCMCを用いたDynamic Linear Modelは重く、カルマンフィルタはノイズがガウス分布に従うという仮定が必要である。
頻度主義の関連研究があるが、実験結果などを素直に組み込みたいのでベイズ主義的な手法を提案する。

## 手法

- $f_{t,p}(x_{t,p})=x_{t,p}^{\beta_{t,p}}$
- $\beta_{t,p}=\sum_j w_j(t)\cdot b_{j,p}$ とGeneralized Additive Model(GAM)を用いる
- $w_j(t)=k(t, t_j)/\sum_{j-1}^J k(t, t_j)$ とカーネル関数 $k(\cdot, \cdot)$ を用いて表現する
- トレンドもGAMを用いて$l_t=\beta_{t,lev}$とする。
- 季節性もGAMを用いて$s_t=X_{t,seas}\beta_{t,seas}$とする。$X_{t,seas}$はフーリエ変換を用いて作ったf seasonality covariate matrixである。
- トレンドと季節性の隠れ変数$b$はラプラス分布を用いてサンプリングする。
- 回帰の隠れ変数$b$はgauss分布を用いた２段階の階層的モデルを用いる。
- トレンドと季節性のカーネルは独自の $K(t, t_l)=1-\frac{|t-t_l|}{|t_{j+1}-t_j|}$
- 回帰はgaussカーネルを用いる

## 実験

- シミュレーションデータで事前知識を用いたらsymmetric mean absolute percentage error (SMAPE) と pinball loss (with 2.5% and 97.5% target quantiles)が改善
- 実データでSARIMAとFacebook Prophetと比較して、SMAPEが改善
