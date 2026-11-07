---
title: "GetObject（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetObject"
---

The get_object API downloads a specified object from the bucket, supporting multiple versions, server\-side encryption, partial downloads, and conditional downloads. This article explains how to use the get_object API in the Rust SDK to download objects.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your specific situation. For details, see [Region and Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure Long-term Access Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Before downloading archived, Cold Archive, or Deep Cold Archive objects, you must first call restore_object to complete restoration.

* When carrying the `range` parameter, the returned `e_tag` is still the `e_tag` of the entire object, not the `e_tag` of a fragment.

* If `response_content_type`, `response_content_disposition`, and other `response_*` parameters are specified, the server will overwrite the corresponding response headers with the specified values.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the get_object operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5LiL6L295pWw5o2u5Yiw5YaF5a2Y"></span>
### Download data to memory

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::{GetObjectInput};
use ve_tos_rust_sdk::error::TosError;
use ve_tos_rust_sdk::asynchronous::object::{ObjectAPI, ObjectContent};

#[derive(Debug, Default)]
pub struct TokioRuntime {}

#[async_trait]
impl AsyncRuntime for TokioRuntime {
    type JoinError = tokio::task::JoinError;
    async fn sleep(&self, duration: Duration) {
        tokio::time::sleep(duration).await;
    }

    fn spawn<'a, F>(&self, future: F) -> BoxFuture<'a, Result<F::Output, Self::JoinError>>
    where
        F: Future + Send + 'static,
        F::Output: Send + 'static,
    {
        Box::pin(Handle::current().spawn(future))
    }

    fn block_on<F: Future>(&self, future: F) -> F::Output {
        Handle::current().block_on(future)
    }
}

#[tokio::main]
async fn main() {
    let _guard = init_tracing_log("info", "temp/logs", "app.log");
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    let bucket = "example-bucket";
    let key = "example-object.txt";
    let input = GetObjectInput::new(bucket, key);
    let output = client.get_object(&input).await;

    match output {
        Ok(mut output) => {
            println!("Request ID: {}", output.request_id());
            let data = String::from_utf8(output.read_all().await.unwrap()).unwrap();
            println!("{}", data);
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } =>
                    println!("Server error: request_id={}, ec={}, code={}", request_id, ec, code),
            }
        }
    }
}
```


<span id=".6IyD5Zu05LiL6L29"></span>
### Range download

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::{GetObjectInput, GetObjectOutput};
use ve_tos_rust_sdk::error::TosError;
use tokio::io::AsyncReadExt;
use ve_tos_rust_sdk::asynchronous::object::{ObjectAPI, ObjectContent};

#[derive(Debug, Default)]
pub struct TokioRuntime {}

#[async_trait]
impl AsyncRuntime for TokioRuntime {
    type JoinError = tokio::task::JoinError;
    async fn sleep(&self, duration: Duration) {
        tokio::time::sleep(duration).await;
    }

    fn spawn<'a, F>(&self, future: F) -> BoxFuture<'a, Result<F::Output, Self::JoinError>>
    where
        F: Future + Send + 'static,
        F::Output: Send + 'static,
    {
        Box::pin(Handle::current().spawn(future))
    }

    fn block_on<F: Future>(&self, future: F) -> F::Output {
        Handle::current().block_on(future)
    }
}

#[tokio::main]
async fn main() {
    let _guard = init_tracing_log("info", "temp/logs", "app.log");
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    let bucket = "example-bucket-2";
    let key = "example-object.txt";
    let mut input = GetObjectInput::new(bucket, key);
    input.set_range("bytes=0-99"); // Download first 100 bytes

    let output = client.get_object(&input).await;

    match output {
        Ok(mut output) => {
            println!("Request ID: {}", output.request_id());
            println!("Content Range: {}", output.content_range());
            let data = String::from_utf8(output.read_all().await.unwrap()).unwrap();
            println!("{}", data);
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } =>
                    println!("Server error: request_id={}, ec={}, code={}", request_id, ec, code),
            }
        }
    }
}
```


<span id=".6YWN572u5a6i5oi356uv6ZmQ6YCf"></span>
### Configure client speed limit

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::{GetObjectInput, GetObjectOutput};
use ve_tos_rust_sdk::error::TosError;
use tokio::io::AsyncReadExt;
use ve_tos_rust_sdk::asynchronous::object::{ObjectAPI, ObjectContent};

#[derive(Debug, Default)]
pub struct TokioRuntime {}

#[async_trait]
impl AsyncRuntime for TokioRuntime {
    type JoinError = tokio::task::JoinError;
    async fn sleep(&self, duration: Duration) {
        tokio::time::sleep(duration).await;
    }

    fn spawn<'a, F>(&self, future: F) -> BoxFuture<'a, Result<F::Output, Self::JoinError>>
    where
        F: Future + Send + 'static,
        F::Output: Send + 'static,
    {
        Box::pin(Handle::current().spawn(future))
    }

    fn block_on<F: Future>(&self, future: F) -> F::Output {
        Handle::current().block_on(future)
    }
}

#[tokio::main]
async fn main() {
    let _guard = init_tracing_log("info", "temp/logs", "app.log");
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    let bucket = "example-bucket";
    let key = "example-object.txt";
    let mut input = GetObjectInput::new(bucket, key);
    input.set_traffic_limit(819200);

    let output = client.get_object(&input).await;

    match output {
        Ok(mut output) => {
            println!("Request ID: {}", output.request_id());
            let data = String::from_utf8(output.read_all().await.unwrap()).unwrap();
            println!("{}", data);
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } =>
                    println!("Server error: request_id={}, ec={}, code={}", request_id, ec, code),
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the GetObject API documentation, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
