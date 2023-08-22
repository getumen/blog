---
title: "Relevance Constrained Re-ranking in Sponsored Listing Recommendations"
date: 2023-08-03T10:47:32+09:00
draft: false
tags: ["AdKDD", "AdKDD 2021", "論文", "EC広告", "貪欲法", "制約付き最適化"]
---

- 学会: AdKDD 2021
- http://papers.adkdd.org/2021/papers/adkdd21-ge-relevance.pdf

## メモ

- 問題設定: ECサイトでスポンサーリスティングありの検索結果表示で、score = p (CV確率) * c (販売コスト) + w (重み) * p (CV確率) * b (広告レート) 順に商品を並び替える
- 課題: 広告の売り上げと商品の販売高にはトレードオフがあり、重みwによって調整できるので、良い感じの重みを動的にチューニングする。
- 関連度順に引いた商品に対するKL-Divergenceを制約として売り上げを最大化する最適化問題として解く。
- KL-Divergenceのを選んだのは、確率は正規化されているので購入確率のスケーリングに影響されないため
- 手法1: KD-Divergenceの制約を満たす限りにおいて、広告収益が最大になるように貪欲なGridSearchでとく
- 手法2: KD-Divergenceを予測する。特徴量は引いた商品の数や総額、PTRスコア、広告料金の要約統計量、重みw(one hot)を用いる。OLSの推論時は $w = \frac{\theta_{KL} - \beta_0 - \sum_{i=0}^{n, i\not=w}x_{i}\cdot\beta_i}{\beta_{w}}$ として重みを決める。GBDTも検討。
- 実験１：固定の重みとKL-Divergenceの予測の比較。予測は優位性は示されなかったが、広告売り上げと商品売り上げのトレードオフを解消できた。
- 実験２：A/Bテストによる比較。予測ベースの手法として、OLSとGBDTを比較するとGBDTが優れていた。GBDTは購入数を変えずに広告売り上げを増やし、貪欲砲は購入数と広告売り上げを増加させた。実装の簡単さからGBDTを本番で採用した。
