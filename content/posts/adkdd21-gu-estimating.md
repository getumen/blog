---
title: "Estimating True Post-Click Conversion via Group-stratified Counterfactual Inference"
date: 2023-08-03T08:43:41+09:00
draft: false
tags: ["AdKDD", "AdKDD 2021", "論文", "因果推論", "CVR予測", "uplift modeling"]
---

- 学会: AdKDD 2021
- http://papers.adkdd.org/2021/papers/adkdd21-gu-estimating.pdf

## メモ

uplift modelingと違うと言っているが、提案手法の中で重要なTCVRはConditinal Average Treatment Effect (CATE)と同じである。また、free rider metricは(CVR-CATE)/CVRである。

## 内容

- TCVR(True Post-Click Conversion)=Conditinal Average Treatment Effect (CATE)を推定する
- free rider metric=(CVR-CATE)/CVRを算出する
- 推定はユーザ埋め込みと広告埋め込みをconcatenatesしたものを共通のレイヤとし、treatmentのあるなしで学習データとDNNモデルを分割して学習する
- 実験結果はよく知られた事実と一致していたらしい
