---
title: "Learning Similarity Preserving Binary Codes for Recommender Systems"
date: 2023-06-21T10:11:26+09:00
draft: false
tags: ["AdKDD", "AdKDD 2022", "論文", "推薦", "Matrix Factorization", "Auto Encoder", "Binary Code"]
---


- 学会: AdKDD 2022
- http://papers.adkdd.org/2022/papers/adkdd22-shi-learning.pdf

## 内容

- 巨大な推薦問題を解くために、ユーザベクトルと商品ベクトルをバイナリーコーディングするのが有用
- 関連研究
  - 行列分解でベクトルを学習してから、バイナリーコーディングする２段階に分けた手法
  - scaled tanh関数を用いて、ベクトルの学習とバイナリーコーディングする。ユーザベクトルや商品ベクトルはAE, VAE, GNNを用いて表し、相互作用はsimilarity lossやrank lossを用いて学習する。
  - cross-modal retrievalではNNを使って特徴量を抽出し、バイナリーコーディングする。
- モデルは3つの損失関数を用いて学習する
  - explicit feedback matrixを auto encoderにより、再構築した時の二乗誤差
  - 異なるモーダリティのエンティティ間の類似度を測るためのMap推定
  - bitがバランスよくなるような損失
- バイナリーコーディングはsign関数を学習が進むごとに`a`が指数的に増える `tanh(a f)` を用いて近似する
- 実験では関連手法よりよかった
