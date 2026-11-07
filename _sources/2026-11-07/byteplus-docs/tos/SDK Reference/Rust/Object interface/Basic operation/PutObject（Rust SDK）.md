---
title: "PutObject（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutObject"
---

The put_object interface uploads objects to a specified bucket, supporting encryption, ACL, storage class, tags, rate limiting, and other configurations. This article explains how to upload using the put_object interface in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, refer to [Regions and Access Domains](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code in this article reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, configure long\-term access credentials. For details, refer to [Configure Long-Term Access Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* When a bucket has versioning enabled, the `forbid_overwrite` setting is invalid, and objects with the same name are always allowed to be overwritten.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the put_object operation, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policy](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5LiK5Lyg5a2X56ym5Liy"></span>
### Upload string

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::tos::{new_stream, BufferStream};
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::{PutObjectInput};
use ve_tos_rust_sdk::asynchronous::tos;
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
    let bucket = "example-bucket-2";

    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    // Upload String
    let data = "Hello, TOS! This is a test string.";
    let stream = new_stream(data);
    let key = "uploaded_string.txt";
    let mut input = PutObjectInput::<BufferStream>::new_with_content(bucket, key, stream);

    let output = client.put_object(&input).await;
    match output {
        Ok(res) => {
            println!("Upload string success");
            println!("request_id: {}", res.request_id());
            println!("etag: {}", res.etag());
            println!("hash_crc64ecma: {}", res.hash_crc64ecma());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server error: request_id={}, ec={}, code={}", request_id, ec, code),
                _ => println!("Unknown error: {:?}", err),
            }
        }
    }
}
```


<span id=".5LiK5Lyg5pe26K6-572u5a-56LGh5YWD5pWw5o2u5L-h5oGv"></span>
### Set object metadata when uploading

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use std::collections::HashMap;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::PutObjectInput;
use ve_tos_rust_sdk::object::BufferStream;
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
    let bucket = "example-bucket";

    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    // Upload with Metadata
    let data = "Data with custom metadata";
    let stream = BufferStream::new(data.as_bytes().into());
    let key = "file_with_metadata.txt";
    let mut input = PutObjectInput::<BufferStream>::new_with_content(bucket, key, stream);

    // Set custom metadata
    let mut meta = HashMap::new();
    meta.insert("author".to_string(), "John Doe".to_string());
    meta.insert("project".to_string(), "TOS SDK Example".to_string());
    meta.insert("version".to_string(), "1.0".to_string());
    input.set_meta(meta);

    // Set additional metadata fields
    input.set_content_type("text/plain");
    input.set_cache_control("max-age=3600");
    input.set_content_disposition("attachment; filename=\"metadata_file.txt\"");

    let output = client.put_object(&input).await;
    match output {
        Ok(res) => {
            println!("Upload with metadata success");
            println!("request_id: {}", res.request_id());
            println!("etag: {}", res.etag());
            println!("hash_crc64ecma: {}", res.hash_crc64ecma());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server error: request_id={{}}, ec={{}}, code={{}}", request_id, ec, code),
                _ => println!("Unknown error: {{:?}}", err),
            }
        }
    }
}
```


<span id=".5LiK5Lyg5pys5Zyw5paH5Lu25rWB"></span>
### Upload local file stream

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use tokio::fs::File;
use tokio_util::io::ReaderStream;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::PutObjectInput;
use ve_tos_rust_sdk::asynchronous::tos;
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
    let bucket = "example-bucket-2";

    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    // Upload Local File
    let file_path = "test_file.txt"; // Replace with actual path
    let file = match tokio::fs::File::open(file_path).await {
        Ok(f) => f,
        Err(e) => {
            println!("Failed to open file: {}", e);
            return;
        }
    };
    let stream  = ReaderStream::new(file);
    let key = "uploaded_file.txt";
    let input = PutObjectInput::<ReaderStream<File>>::new_with_content(bucket, key, stream);

    let output = client.put_object(&input).await;
    match output {
        Ok(res) => {
            println!("Upload local file success");
            println!("request_id: {}", res.request_id());
            println!("etag: {}", res.etag());
            println!("hash_crc64ecma: {}", res.hash_crc64ecma());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server error: request_id={}, ec={}, code={}", request_id, ec, code),
                _ => println!("Unknown error: {:?}", err),
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For API documentation about PutObject, see [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject).
