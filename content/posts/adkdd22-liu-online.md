---
title: "Online Meta-Learning for Model Update Aggregation in Federated Learning for Click-Through Rate Prediction"
date: 2023-06-20T12:57:30+09:00
draft: false
tags: ["AdKDD", "AdKDD 2022", "論文", "Federated Learning", "Meta Learning", "CTR予測", "オンライン学習"]
---

- 学会: AdKDD 2022
- http://papers.adkdd.org/2022/papers/adkdd22-liu-online.pdf


## 内容

- Federated Learningはクライアントごとの性質の違い(client drift)によって、学習が遅くなったり、良い解に収束しなかったりする
- クライアントの異質さに適合し、学習プロセスと学習パラメータごとに適合するMetaUAを提案する
- クライアントの重要度とサーバサイドの学習率のスケーリングパラメータをオンライン学習する
- こうしたパラメータの勾配は連鎖律により求められる
- 追加で必要なコミュニケーションコストは各クライアントの勾配であり、これを減らせる手法は２〜３個しかないのであっても良いはず
- 追加の計算はFLでSGDを回しているので、それに比べたら小さい
- ストレージはユーザの人口が多いので必要
- 実験ではFedAvgやFedAdagradより良いことを示した
