---
title: "My Awesome Rust: thiserror"
date: 2024-01-04T14:59:32+09:00
draft: false
---

Rustで独自のエラーを自作する際に以下のようなやらないといけないことが多くあり、面倒です。

- `std::error::Error` traitを実装
- 読みやすいエラーログを作るために `Display` traitを実装
- 他のエラーなどからの変換を容易にするために `From<T>` traitを実装

また、エラーは構造体だったり、列挙型だと便利であることが多いです。
`thiserror` はこうしたエラーの自作を便利にするライブラリです。

## 使い方

`thiserror` はCargo.tomlに依存として追加することで使えるようになります。

```toml
[dependencies]
thiserror = "1"
```

以下はドキュメント(https://docs.rs/thiserror/latest/thiserror/)にある実装例の一つです。


```rust
use thiserror::Error;

#[derive(Error, Debug)]
pub enum DataStoreError {
    #[error("data store disconnected")]
    Disconnect(#[from] io::Error),
    #[error("the data for key `{0}` is not available")]
    Redaction(String),
    #[error("invalid header (expected {expected:?}, found {found:?})")]
    InvalidHeader {
        expected: String,
        found: String,
    },
    #[error("unknown data store error")]
    Unknown,
}
```

- `Disconnect`では `error`という属性でDisplayトレイトを`"data store disconnected"`というエラーメッセージで実装しています。また、`io::Error`に対するFromトレイトを実装しています。
- Redactionでは `error`という属性でDisplayトレイトを実装する際にタプルの値を利用しています。`#[error("{0}")] ⟶ write!("{}", self.0)` という意味なので、０番目の値のDisplayトレイトの実装を呼び出しています。
- InvalidHeaderでは、`expected`と`found`のDebugトレイトの実装を呼び出してエラーメッセージを作成しています。`#[error("{var:?}")] ⟶ write!("{:?}", self.var)`という意味を表しています。

エラーをラップしていくために`source`や`backtrace`といった属性が用意されていますが、個人的にはanyhowを使えば良い気がしています。
