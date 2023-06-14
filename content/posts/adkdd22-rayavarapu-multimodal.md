---
title: "Multimodal Transformers for Detecting Bad Quality Ads on
YouTube"
date: 2023-06-14T12:44:04+09:00
draft: false
tags: ["AdKDD", "AdKDD 2022", "論文", "Trust & Safety", "Transformer", "BERT", "MultiModal"]
---


- 学会: AdKDD 2022
- http://papers.adkdd.org/2022/papers/adkdd22-rayavarapu-multimodal.pdf

## 内容

- Youtubeのビデオ広告の審査をマルチモーダルのDNNでやった
- 正解ラベルは人手でつけたbad ads rate
- 広告タイトルと説明をBERTに入れた
- 動画を60フレームサンプリングして、ResNetに入れた
- 文字列特徴量と画像特徴量をいつマージするかで、Early Fusion、Mid Fusion、Late Fusionを試したら、Mid Fusionが良かった。
    - Early Fusion: 各特徴量をすぐにconcatenateしてAverage Pooling
    - Mid Fusion: 各特徴量ごとにSelf-Attension Layerを何層か噛ませてからConcatenateして、Co-Attension Layerを何層か噛ませてAverage Pooling
    - Late Fusion: 各特徴量ごとにSelf-Attension Layerを何層か噛ませてからAverage Pooling
