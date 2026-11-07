---
title: "ListObjectsType2（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/ListObjectsType2"
---

The list_objects_type2 interface is used to list objects in a bucket.

<span id="916fffd1"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code in this article reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* A single request returns up to 1000 objects. You can use the `max-keys` parameter to set the number of returned objects.


<span id="a4809439"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you want to perform the list_objects_type2 operation using a sub\-account, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:ListBucket

<span id=".5Luj56CB56S65L6L"></span>
## Code examples

<span id="0e9ea517"></span>
### Simple listing

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::ListObjectsType2Input;
use ve_tos_rust_sdk::error::TosError;

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

    let bucket_name = "example-bucket";
    let mut input = ListObjectsType2Input::new(bucket_name);
    let output = client.list_objects_type2(&input).await;

    match output {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            println!("Total objects: {}", output.key_count());
            output.contents().iter().enumerate().for_each(|(idx, obj)| {
                println!("Object {}:", idx + 1);
                println!("  Key: {}", obj.key());
                println!("  Size: {} bytes", obj.size());
                obj.last_modified().map(|lm| println!("  Last Modified: {}", lm));
                println!("  ETag: {}", obj.etag());
            });
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client Error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server Error: RequestID={}, Code={}, Message={}", request_id, code, ec),
                _ => println!("Unexpected Error: {:?}", err)
            }
        }
    }
}
```


<span id=".5YiG6aG15YiX5Li-5qG25YaF5a-56LGh"></span>
### List objects in the bucket with pagination

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::ListObjectsType2Input;
use ve_tos_rust_sdk::error::TosError;

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

    let bucket_name = "example-bucket";
    let page_size = 10;
    let mut continuation_token: Option<String> = None;
    let mut page_number =1;

    loop {
        let mut input = ListObjectsType2Input::new(bucket_name);
        input.set_max_keys(page_size as isize);
        if let Some(token) = &continuation_token {
            input.set_continuation_token(token.clone());
        }

        let output = client.list_objects_type2(&input).await;
        match output {
            Ok(output) => {
                println!("Page {} - Request ID: {}", page_number, output.request_id());
                println!("Page {} - Objects count: {}", page_number, output.key_count());
                output.contents().iter().enumerate().for_each(|(idx, obj)| {
                    println!("Page {} Object {}: {}", page_number, idx+1, obj.key());
                });

                if !output.is_truncated() {
                    println!("Page {} - No more pages.", page_number);
                    break;
                }

                continuation_token = Some(output.next_continuation_token().to_string());
                println!("Page {} - Next token: {}", page_number, continuation_token.as_ref().unwrap());
                page_number += 1;
            }
            Err(err) => {
                println!("Page {} - Error: {:?}", page_number, err);
                break;
            }
        }
    }
}

```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5a-56LGh"></span>
### List objects with a specified prefix

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::ListObjectsType2Input;
use ve_tos_rust_sdk::error::TosError;

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

    let bucket_name = "example-bucket";
    let mut input = ListObjectsType2Input::new(bucket_name);
    input.set_prefix("docs/");
    let output = client.list_objects_type2(&input).await;

    match output {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            println!("Filtered objects count: {}", output.key_count());
            output.contents().iter().enumerate().for_each(|(idx, obj)| {
                println!("Filtered Object {}:", idx +1);
                println!("  Key: {}", obj.key());
                println!("  Size: {} bytes", obj.size());
            });
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client Error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server Error: RequestID={}, Code={}, Message={}", request_id, code, ec),
                _ => println!("Unexpected Error: {:?}", err)
            }
        }
    }
}

```


<span id=".566A5Y2V5YiX5Li-"></span>
### Related documentation

For API documentation about ListObjectsType2, see [ListObjectsV2](https://docs.byteplus.com/docs/tos/reference-listobjectsv2).
