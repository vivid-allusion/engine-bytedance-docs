---
title: "CopyObject（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/CopyObject"
---

The copy_object interface copies objects within the same region, either between the same bucket or different buckets. This article explains how to use the copy_object interface in the Rust SDK to copy objects, supporting metadata replacement, server\-side encryption, and version control.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to provide the region and endpoint in the sample code according to your actual situation. For detailed information, see [region and endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Before using the SDK, you need to configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* If the source object size exceeds 5 GiB, use the upload_part_copy interface instead, as copy_object only supports sizes between 0 and 5 GiB.

* If the source object is stored as ARCHIVE, COLD_ARCHIVE, or DEEP_COLD_ARCHIVE, perform a restore operation before calling copy_object.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, but IAM users have no permissions by default. If a sub\-account needs to perform the copy_object operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policy](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5ZCM5LiA5qG25YaF5aSN5Yi25a-56LGh"></span>
### Copy object within the same bucket

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::{CopyObjectInput, PutObjectFromBufferInput};
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

    // Upload source object
    let source_key = "source-object.txt";

    // Same bucket copy
    let copy_input = CopyObjectInput::new("example-bucket", "copied-object.txt", "example-bucket", source_key);
    let output = client.copy_object(&copy_input).await;
    match output {
        Ok(res) => {
            println!("Copy object succeeded");
            println!("etag: {}", res.etag());
            if let Some(lm) = res.last_modified() { println!("last_modified: {}", lm); }
            println!("copy_source_version_id: {}", res.copy_source_version_id());
            println!("version_id: {}", res.version_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code),
                _ => println!("Unknown error: {:?}", err)
            }
        }
    }
}
```


<span id=".5aSN5Yi25a-56LGh5bm26K6-572u5YWD5pWw5o2u"></span>
### Copy object and set metadata

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::{CopyObjectInput, PutObjectFromBufferInput};
use ve_tos_rust_sdk::enumeration::MetadataDirectiveType;
use std::collections::HashMap;
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

    // Upload source object
    let source_key = "source-object.txt";

    // Copy with metadata
    let mut copy_input = CopyObjectInput::new("example-bucket", "copied-with-metadata.txt", "example-bucket", source_key);
    let mut meta = HashMap::new();
    meta.insert("author".to_string(), "TOS Team".to_string());
    meta.insert("category".to_string(), "document".to_string());
    copy_input.set_meta(meta);
    copy_input.set_metadata_directive(MetadataDirectiveType::MetadataDirectiveReplace);

    let output = client.copy_object(&copy_input).await;
    match output {
        Ok(res) => {
            println!("Copy with metadata succeeded");
            println!("etag: {}", res.etag());
            if let Some(lm) = res.last_modified() { println!("last_modified: {}", lm); }
            println!("copy_source_version_id: {}", res.copy_source_version_id());
            println!("version_id: {}", res.version_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code),
                _ => println!("Unknown error: {:?}", err)
            }
        }
    }
}
```


<span id=".6Leo5qG25aSN5Yi25a-56LGh"></span>
### Copy object across buckets

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::{CopyObjectInput};
use ve_tos_rust_sdk::bucket::CreateBucketInput;
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

    // Upload source object
    let source_key = "source-object.txt";
    // Cross bucket copy
    let copy_input = CopyObjectInput::new("target-bucket", "copied-object.txt", "example-bucket", source_key);
    let output = client.copy_object(&copy_input).await;
    match output {
        Ok(res) => {
            println!("Cross bucket copy succeeded");
            println!("etag: {}", res.etag());
            if let Some(lm) = res.last_modified() { println!("last_modified: {}", lm); }
            println!("copy_source_version_id: {}", res.copy_source_version_id());
            println!("version_id: {}", res.version_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code),
                _ => println!("Unknown error: {:?}", err)
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of CopyObject, see [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).
