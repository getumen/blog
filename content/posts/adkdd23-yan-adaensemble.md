---
title: "AdaEnsemble: Learning Adaptively Sparse Structured Ensemble Network for Click-Through Rate Prediction"
date: 2023-08-22T16:33:07+09:00
draft: false
tags: ["AdKDD", "AdKDD 2023", "論文", "CTR予測"]
---

- 学会: AdKDD 2023
- http://papers.adkdd.org/2023/papers/adkdd23-yan-adaensemble.pdf

実験を見て、FMやDCNと大差ないので途中で読むのをやめました。
実務で保守コストを含めて考えると、シンプルなMLPに意味のある特徴量と大量のデータを入れた方がアーキテクチャを複雑にするより性能が良いので・・・

## 内容

- Sparse MoE (Mixture of Experts)層を提案
- Sparse MoE層を重ねる際に最適な深さを適応的に学習する仕組みを提案
- FMやWide&Deep、DCN v2を上回る性能
- ソースコード：[https://github.com/yanyachen/AdaEnsemble](https://github.com/yanyachen/AdaEnsemble)


