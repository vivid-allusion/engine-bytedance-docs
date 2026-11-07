---
title: "Install Rust SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Install_Rust_SDK"
---

Before running the TOS Rust SDK, you need to install the SDK first. This document provides the SDK's runtime environment requirements and various installation methods.

<span id="fd87e1de"></span>
## Prerequisites

Before installing the SDK, you need to set up the Rust development environment. You can complete the environment setup by following the [Rust official website](https://rust-lang.org/tools/install/) instructions.

After installation, use the `cargo version` command to check the version information.

<span id="30308d4c"></span>
## SDK download links


* Latest source code: [source code link](https://github.com/volcengine/ve-tos-rust-sdk)

* Version revision history: [version history](https://github.com/volcengine/ve-tos-rust-sdk/blob/main/CHANGELOG.md)

* Legacy versions: [legacy versions](https://github.com/volcengine/ve-tos-rust-sdk/releases)


<span id="c47d6555"></span>
## Installation methods

TOS Rust SDK uses https://crates.io/ to manage packages. After setting up the development environment and Rust project, you can add dependencies using `cargo` as follows:

```Rust
cargo add ve-tos-rust-sdk -F tokio-runtime
```


You can also add the TOS Rust SDK dependency directly in the Cargo.toml file as follows:

```Rust
[dependencies]
ve-tos-rust-sdk = { version = "2.9.2", features = ["tokio-runtime"] }
```
