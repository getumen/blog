---
title: "Modeling labels for conversion value prediction"
date: 2023-07-31T08:22:06+09:00
draft: false
tags: ["AdKDD", "AdKDD 2021", "論文", "value予測", "ROAS"]
---

- 学会: AdKDD 2021
- http://papers.adkdd.org/2021/papers/adkdd21-badanidiyuru-modeling.pdf

## 内容

- コンバージョン価値予測の課題
  1. 広告主ごとにコンバージョン価値のスケールが違う
  2. 外れ値へ過学習する
  3. 平均値ではなく、分布を予測したい
- 問題設定：クリックに紐づくCV価値の総和$\ell$を予測する
- 課題1の解決策：ラベルを正規化する。広告主$A$毎に０より大きい値を取るラベルの平均$\eta_A$を求めて、$\ell/\eta_A$を予測する。最終的な予測値は$\eta_A E[\ell| X, A]$
- 課題2の解決策：
  1. ラベルの正規化にwinsorized mean (minとmaxをそれぞれ隣接する値で置き換えることで、外れ値の影響を緩和した平均値)を用いたラベルを予測するヘッドを追加する。
  2. winsorized meanではない平均を用いた方のヘッド（予測に使う方）の目的関数はdown-weightをかける。
- 課題3の解決策：zero inflated poisson regressionを用いる -> うまくいかなかった。labelが0かどうかを判定するヘッドを追加する -> うまく行った。
- 更なる性能改善のために、$E[l|A, l>0]$ の分位数で bucketized し、それぞれのバケット内で予測するための softmax headを追加する。
- 実験
  - 正規化によりポアソン対数尤度が改善したが、期待CV価値の分位点ごとに見るとCV価値が小さい部分で大きなバイアスが生じていた。
  - ablation studyを見ると、winsorized meanを用いた方のヘッドが最も重要そう。

