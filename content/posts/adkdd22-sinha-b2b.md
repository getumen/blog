---
title: "B2B Advertising: Joint Dynamic Scoring of Account and Users"
date: 2023-06-15T17:41:16+09:00
draft: false
tags: ["AdKDD", "AdKDD 2022", "論文", "B2B", "行動ターゲティング", "group decision making"]
---

- 学会: AdKDD 2022
- http://papers.adkdd.org/2022/papers/adkdd22-sinha-b2b.pdf

## 内容

- B2B広告ではアカウント（会社）ごとにコンバージョンが発生するが、アカウントに所属する社員（個人）に営業をかける
- グループ内の意思決定を個人の行動から予測するgroup decision making問題を考える
- アカウントが５週間以内にコンバージョンするかを予測する
- 特徴量は以下の通り
  - 社員の行動（open email, click email, send email, unsubscribe email, open sales email, click sales email, send sales email, forwarded email received, forwarded email sent）
  - 社員の属性（source of arrival, opt out of email, opt out of phone）
  - アカウントの属性（revenue, number of employees）
- モデルは以下の通り
  1. 行動を週ごとに埋め込む (GRU)
  2. 週ごとの埋め込みを個人ごとに埋め込む (GRU)
  3. FC(2 + 社員の属性)
  4. FC(3 + アカウントの属性)
  5. p(prospect conversion | 4)
