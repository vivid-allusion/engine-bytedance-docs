---
title: "DeleteMultiObjects（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteMultiObjects"
---

The delete_multi_objects API deletes multiple objects in a bucket, up to 1000 per request. This article explains how to use the delete_multi_objects API in the Rust SDK for batch deletion, supporting version control and quiet mode.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the example code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leaks, the example code reads Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, configure long\-term access credentials. For details, see [configuring long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Each call deletes up to 1000 objects; delete in batches if exceeded.

* If version control is enabled on the bucket and no `version_Id` is provided, the system inserts a `delete_marker` instead of permanently deleting.

* `recursive` and `skip_trash` apply only to hierarchical namespaces with recycle bins enabled; they are ignored for standard buckets.

* When `quiet` is set to `true`, the response only returns entries that failed to delete. No entries indicate all succeeded.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have none by default. If you need to use a sub\-account to perform the delete_multi_objects operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteMultiObjects

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5om56YeP5Yig6Zmk5a-56LGh"></span>
### Batch delete objects

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
use ve_tos_rust_sdk::object::{DeleteMultiObjectsInput, ObjectTobeDeleted};
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

    // Batch delete objects
    let bucket = "example-bucket";
    let objects = vec![
        ObjectTobeDeleted::new("obj1"),
        ObjectTobeDeleted::new("obj2"),
        ObjectTobeDeleted::new("obj3"),
    ];
    let input = DeleteMultiObjectsInput::new_with_objects(bucket, objects);

    let output = client.delete_multi_objects(&input).await;
    match output {
        Ok(output) => {
            println!("Deleted objects:");
            for (index, deleted) in output.deleted().iter().enumerate() {
                println!("[{}] Key: {}, VersionId: {}, DeleteMarker: {}, DeleteMarkerVersionId: {}",
                         index, deleted.key(), deleted.version_id(), deleted.delete_marker(), deleted.delete_marker_version_id());
            }
            println!("Errors:");
            for (index, error) in output.error().iter().enumerate() {
                println!("[{}] Key: {}, VersionId: {}, Code: {}, Message: {}",
                         index, error.key(), error.version_id(), error.code(), error.message());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: message: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".5om56YeP5Yig6Zmk5oyH5a6a54mI5pys55qE5a-56LGh"></span>
### Batch delete objects with specified versions

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
use ve_tos_rust_sdk::object::{DeleteMultiObjectsInput, ObjectTobeDeleted};
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

    // Batch delete objects with specified versions
    let bucket = "example-bucket";
    let objects = vec![
        ObjectTobeDeleted::new_with_version_id("obj1", "version1"),
        ObjectTobeDeleted::new_with_version_id("obj2", "version2"),
    ];
    let input = DeleteMultiObjectsInput::new_with_objects(bucket, objects);

    let output = client.delete_multi_objects(&input).await;
    match output {
        Ok(output) => {
            println!("Deleted objects:");
            for (index, deleted) in output.deleted().iter().enumerate() {
                println!("[{}] Key: {}, VersionId: {}, DeleteMarker: {}, DeleteMarkerVersionId: {}",
                         index, deleted.key(), deleted.version_id(), deleted.delete_marker(), deleted.delete_marker_version_id());
            }
            println!("Errors:");
            for (index, error) in output.error().iter().enumerate() {
                println!("[{}] Key: {}, VersionId: {}, Code: {}, Message: {}",
                         index, error.key(), error.version_id(), error.code(), error.message());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: message: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".6K6-572u5Li66Z2Z6buY5qih5byP5om56YeP5Yig6Zmk5a-56LGh"></span>
### Set batch delete objects to silent mode

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
use ve_tos_rust_sdk::object::{DeleteMultiObjectsInput, ObjectTobeDeleted};
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

    // Batch delete objects in quiet mode
    let bucket = "example-bucket";
    let objects = vec![
        ObjectTobeDeleted::new("obj1"),
        ObjectTobeDeleted::new("obj2"),
        ObjectTobeDeleted::new("obj3"),
    ];
    let mut input = DeleteMultiObjectsInput::new_with_objects(bucket, objects);
    input.set_quiet(true);

    let output = client.delete_multi_objects(&input).await;
    match output {
        Ok(output) => {
            println!("Deleted objects (only errors are shown in quiet mode):");
            println!("Errors:");
            for (index, error) in output.error().iter().enumerate() {
                println!("[{}] Key: {}, VersionId: {}, Code: {}, Message: {}",
                         index, error.key(), error.version_id(), error.code(), error.message());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: message: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For API documentation about DeleteMultiObjects, see [DeleteMultiObjects](https://docs.byteplus.com/docs/tos/reference-deletemultiobjects).
