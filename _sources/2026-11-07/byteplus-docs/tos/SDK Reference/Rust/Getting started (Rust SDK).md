---
title: "Getting started (Rust SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getting_started_Rust_SDK"
---

This article explains how to use the TOS Rust SDK for common operations such as creating buckets, uploading, downloading, and deleting objects.

<span id="a0b34eda"></span>
## Create a Bucket

A bucket is a globally unique namespace in TOS, serving as a container to store object data. The following code shows how to create a new bucket.

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
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
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let tos_client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_connections(1024)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build()
        .unwrap();

    let bucket = "bucketname";
    let input = CreateBucketInput::new(bucket);
    let output = tos_client.create_bucket(&input).await;
    match output {
        Ok(output) => {
            println!("request_id: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("message: {}", message);
                }
                TosError::TosServerError { request_id, ec, .. } => {
                    println!("request_id: {}, ec: {}", request_id, ec);
                }
            }
        }
    }
}
```


<span id="30fc7789"></span>
## Upload objects

After successfully creating a new bucket, you can upload objects into the bucket. The code below uploads a string to a TOS bucket.

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::error::TosError;
use ve_tos_rust_sdk::object::PutObjectFromBufferInput;

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
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let tos_client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_connections(1024)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build()
        .unwrap();

    let bucket = "bucketname";
    let key = "objectkey";
    let mut input = PutObjectFromBufferInput::new(bucket, key);
    // 设置对象内容
    input.set_content("hello world");
    let output = tos_client.put_object_from_buffer(&input).await;
    match output {
        Ok(output) => {
            println!("request_id: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("message: {}", message);
                }
                TosError::TosServerError { request_id, ec, .. } => {
                    println!("request_id: {}, ec: {}", request_id, ec);
                }
            }
        }
    }
}
```


<span id="e6a0b421"></span>
## Download objects

The following example demonstrates how to download an object from a bucket into memory.

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use futures_util::StreamExt;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::error::TosError;
use ve_tos_rust_sdk::object::GetObjectInput;

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
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let tos_client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_connections(1024)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build()
        .unwrap();

    let bucket = "bucketname";
    let key = "objectkey";
    let input = GetObjectInput::new(bucket, key);
    let output = tos_client.get_object(&input).await;
    match output {
        Ok(mut output) => {
            println!("request_id: {}", output.request_id());
            // 读取对象内容到内存
            let mut buf = Vec::new();
            loop {
                match output.next().await {
                    None => break,
                    Some(result) => {
                        let x = result.unwrap();
                        buf.extend_from_slice(x.slice(0..x.len()).as_ref());
                    }
                }
            }
            println!("{}", String::from_utf8(buf).unwrap());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("message: {}", message);
                }
                TosError::TosServerError { request_id, ec, .. } => {
                    println!("request_id: {}, ec: {}", request_id, ec);
                }
            }
        }
    }
}
```


<span id="1bfcab58"></span>
## List objects

The following displays the objects that have been uploaded from the bucket.

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::error::TosError;
use ve_tos_rust_sdk::object::ListObjectsType2Input;

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
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let tos_client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_connections(1024)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build()
        .unwrap();

    let bucket = "bucketname";
    let input = ListObjectsType2Input::new(bucket);
    let output = tos_client.list_objects_type2(&input).await;
    match output {
        Ok(output) => {
            println!("request_id: {}", output.request_id());
            for content in output.contents() {
                println!("content: {}, size: {}", content.key(), content.size());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("message: {}", message);
                }
                TosError::TosServerError { request_id, ec, .. } => {
                    println!("request_id: {}, ec: {}", request_id, ec);
                }
            }
        }
    }
}
```


<span id="339ca334"></span>
## When you delete an object

The following code demonstrates deleting an object from the bucket.

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::error::TosError;
use ve_tos_rust_sdk::object::DeleteObjectInput;

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
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let tos_client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_connections(1024)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build()
        .unwrap();

    let bucket = "bucketname";
    let key = "objectkey";
    let input = DeleteObjectInput::new(bucket, key);
    let output = tos_client.delete_object(&input).await;
    match output {
        Ok(output) => {
            println!("request_id: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("message: {}", message);
                }
                TosError::TosServerError { request_id, ec, .. } => {
                    println!("request_id: {}, ec: {}", request_id, ec);
                }
            }
        }
    }
}
```
