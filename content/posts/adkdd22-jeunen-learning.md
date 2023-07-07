---
title: "Learning to Bid with AuctionGym"
date: 2023-07-06T16:57:25+09:00
draft: false
tags: ["AdKDD", "AdKDD 2022", "論文", "Auction", "強化学習", "因果推論", "バンディットアルゴリズム"]
---

- 学会: AdKDD 2022
- http://papers.adkdd.org/2022/papers/adkdd22-jeunen-learning.pdf

## 内容

- セカンドプライスオークションは強い仮定のもとでは真の価値を入札すれば最適戦略
  - 文脈が与えられた時の期待価値を入札者が知っている
  - 提示された入札額が商品の価値に影響しない
  - 競合の入札者は全員同じ情報にアクセスできる
  - オークションの繰り返しで統計的に独立 (https://arxiv.org/abs/2011.09365)
- 現実の広告オークションでは仮定が成り立たないため最適戦略にならないため、SSPはファーストプライスオークションに移行している。
- 「入札額学習問題」を定式化して、強化学習により解く
- 入札額学習問題
  1. 広告アロケーション問題: 文脈（デモグラやプレースメント等）が与えられた時、文脈に対して配信可能な広告から期待社会的余剰を最大化する広告を選択する
  2. 入札問題: 文脈と広告が与えられた時、DSPは入札額を決める、Utilityを最大化するポリシーを学習する。学習方法はDirect MethodとInverse Propensity Scoringの2つがあるが、Doubly Robust Estimatorを提案。
- ポリシーをオンラインで検証するのはコストが高いので、オフライン検証基盤のAuctionGymを提案
  1. インプレッション機会として、文脈をサンプリング
  2. オークション開催者は入札者にオークション機会を提示
  3. 入札者は広告と入札額を決める
  4. オークション開催者は勝者とか金額を決める
  5. 勝った入札者にコンバージョンイベントが確率的に発生
- CVの生成方法: 広告ごとにロジスティック回帰モデルでCV確率を決める。D次元のモデルで決めるが、文脈はk(< D)次元であり、一部のパラメータと文脈は隠されている。
- Bidderのシミュレーション方法: Direct Method, Inverse Propensity Scoring, Doubly Robust Estimatorの3つを実装
- Auctionのシミュレーション: soft&hardなreserve price付きのファーストプライス&セカンドプライスオークションを実装
- 関心のあるメトリック
  - ROAS
  - 社会的余剰のリグレット
  - 入札額の上振れにより失った利得のリグレット
  - 入札額の下振れにより失った利得のリグレット
実験
- RQ1: 2nd price auctionから1st price auctionに移行した影響
  - 特に書いていなかった？（1st price auctionだと期待２位価格を入札するのが最適なので、真のvalueを入札するよりThompson samplingのほうが広告主利得が多いことが図１からわかる）
- RQ2: 最適な広告アロケーションに比べて、学習による影響は？
  - モデルベースのアプローチは直ぐに収束するが、最適ではない（1st price auctionだと期待２位価格を入札するのが最適なので、2nd price auctionの最適戦略と比べてはダメなのでは？）
- RQ3: 社会的メトリックへのEstimatorの影響
  - Doubly Robust Estimatorが最も良い
- 個別のメトリックへのEstimatorの影響
  - Direct MethodはVarianceが低い代わりにバイアスが高く、収束は早いが、入札額が上振れ傾向
  - Inverse Propensity Scoringはバイアスが低いが、Varianceが高く、入札額は上振れ傾向にないが、100万反復後も下振れ傾向にある
  - Doubly Robust EstimatorはROASが高く、入札額は上振れ傾向にない
