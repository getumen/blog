---
title: "Dynamic collaborative filtering Thompson Sampling for cross-domain advertisements recommendation"
date: 2023-06-13T10:23:18+09:00
draft: false
tags: ["AdKDD", "AdKDD 2022", "論文", "推薦", "バンディットアルゴリズム"]
---

- 学会: AdKDD 2022
- https://www.adkdd.org/Papers/Dynamic-collaborative-filtering-Thompson-Sampling-for-cross-domain-advertisements-recommendation/2022

## 内容

- 色々なドメインの知識を転移させて、推薦システムを作りたい。
- トンプソンサンプリングでは自身のアームの結果を用いて `Beta(Σclick, Σ(imp - click))` で事後分布を推定する。
- 提案手法ではユーザのコサイン類似度 `S(u, v)` を用いて自身以外の報酬を重み付ける。つまり、`Beta(Σ S(u, v)*click, Σ S(u, v)*(imp - click))` で事後分布を推定する。

