---
title: "My Awesome Rust: anyhow"
date: 2024-01-03T18:37:17+09:00
draft: false
---

anyhow (https://github.com/dtolnay/anyhow) はRustのエラー処理を扱うライブラリです。
anyhowを使うことで、Go言語にあるエラーのラップを行えるようになります。

## 使い方

anyhowはCargo.tomlに依存として追加することで使えるようになります。

```toml
[dependencies]
anyhow = { version = "1", features = ["backtrace"] }
```

エラーをラップするには以下のようにContextというトレイトに生えているメソッドを使います。
`context`を使うよりも`with_context`を使う方が好ましいです。`with_context`を使えば、エラー発生時のみ引数が評価されるので、`format!`などでエラーメッセージを作るときに不要な評価をなくすことができます。

```rust
use anyhow::Context as _;
use std::fs::File;

fn main() -> anyhow::Result<()> {
    
    let f = File::create("/tmp/test").context("fail to open file")?;
    let f = File::create("/tmp/test").with_context(|| "fail to open file")?;
    
    Ok(())
}
```

backtraceを有効にすると、エラーのデバッグフォーマットにbacktraceが表示されてデバッグしやすくなります。

```console
Error: Failed to read instrs from ./path/to/instrs.json

Caused by:
    No such file or directory (os error 2)

Stack backtrace:
   0: <E as anyhow::context::ext::StdError>::ext_context
             at /git/anyhow/src/backtrace.rs:26
   1: core::result::Result<T,E>::map_err
             at /git/rustc/src/libcore/result.rs:596
   2: anyhow::context::<impl anyhow::Context<T,E> for core::result::Result<T,E>>::with_context
             at /git/anyhow/src/context.rs:58
   3: testing::main
             at src/main.rs:5
   4: std::rt::lang_start
             at /git/rustc/src/libstd/rt.rs:61
   5: main
   6: __libc_start_main
   7: _start
```