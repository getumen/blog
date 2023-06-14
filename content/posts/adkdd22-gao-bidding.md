---
title: "Bidding Agent Design in the LinkedIn Ad Marketplace"
date: 2023-06-14T10:06:34+09:00
draft: false
tags: ["AdKDD", "AdKDD 2022", "論文", "自動入札", "オンライン学習", "凸最適化", "制約付き凸最適化"]
---

- 学会: AdKDD 2022
- http://papers.adkdd.org/2022/papers/adkdd22-gao-bidding.pdf

## 内容

自動入札をオンライン最適化アルゴリズムのFTRLで解くという論文

入札確率の累積分布は狭義単調増加＋log-concave、期待支払額は広義単調増加、requestの総数はわかっているという仮定のもと

- 予算制約 (Sec. 3)
- 目標result単価 where resultはコンバージョン、クリック、viewableインプレッション (Sec. 4.1)
- 期間指定予算消化 (Sec. 4.2)
- 期間指定result保証 (Sec. 4.3)

といった制約を統一的に解くことができるフレームワークを提案。

統一的に解けるので、制約の組み合わせも解ける。

制約をラグランジュの未定乗数法で表現した価値最大化目的関数をFTRLで解く。

LinkedInのオンライン予算分割A/Bテストにおいて、フィードバック制御に比べて8.25%ROIが改善。

## 省略した内容

- 面（やターゲティングなど）ごとの配信
- cold start問題対応
- ミニバッチ更新
