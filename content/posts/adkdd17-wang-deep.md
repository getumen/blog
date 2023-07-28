---
title: "Deep & Cross Network for Ad Click Predictions"
date: 2023-07-27T15:37:55+09:00
draft: false
tags: ["AdKDD", "AdKDD 2017", "論文", "CTR予測", "Factorization Machines"]
---

- 学会: AdKDD 2017
- http://papers.adkdd.org/2017/papers/adkdd17-wang-deep.pdf

## 内容

- Factorization Machinesの一般化であるCross Networkを提案
- $x_{l+1}=x_0x_{l}^{T}w_{l}+b_{l}+x_{l}$をCross networkと呼ぶ。$x_0$は入力、$x_{l}$は$l$番目のCross Layerの出力、$w_{l}$は重み、$b_{l}$はバイアスである。
- Deep Cross NetworkはCross Networkを複数重ねたものとDeep Networkを重ねたものをstackしたものである。
- 実験ではDeep Crossing(DC), DNN, Factorization Machines(FM), Logistic Regression(LR)と比較してloglossが改善した。