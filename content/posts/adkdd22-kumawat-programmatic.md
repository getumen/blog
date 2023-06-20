---
title: "Programmatic optimization of ad pods for maximizing consumer engagement and revenue"
date: 2023-06-19T21:50:05+09:00
draft: false
tags: ["AdKDD", "AdKDD 2022", "論文", "制約付き最適化", "ナップサック問題", "動的計画法", "進化計算", "貪欲法", "RTB", "SSP", "動画広告"]
---

- 学会: AdKDD 2022
- http://papers.adkdd.org/2022/papers/adkdd22-kumawat-programmatic.pdf

## 内容

- Connected Television (CTV) の広告は Ad-podsという動画広告の集合を連続して再生することで行われる
- Ad-podsは再生する広告の時間の合計が枠内であるという制約がある
- Ad-podsは再生する広告は同じIAB広告カテゴリを含んではいけないという制約がある
- Ad-podsは再生する広告は同じドメインの広告を含んではいけないという制約がある
- これはDuration D内に、広告カテゴリとドメインの制約を満たしながら、売上を最大化する制約付きナップサック問題として定式化できる
- 解法1: 動的計画法。厳密解が得られるが、指数オーダの計算量。
- 解法2: 進化計算。
- 解法3: 貪欲法。時間制約、広告カテゴリとドメインの制約を満たす広告を時間あたりの価格が高い順に入れていく。
- 実験で解の質は進化計算より貪欲方がよかった
