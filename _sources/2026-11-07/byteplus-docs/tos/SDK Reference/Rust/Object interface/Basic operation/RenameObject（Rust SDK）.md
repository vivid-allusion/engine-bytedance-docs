---
title: "RenameObject（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/RenameObject"
---

The rename_object API renames objects and updates the modification time. This article explains how to rename objects using the rename_object API in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code based on your situation. For details, see [Region and Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configuring Long-Term Access Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Rename conflicts with version control; buckets with version control enabled cannot call rename_object.

* Rename only affects new objects uploaded after the feature is enabled and does not apply to existing objects (except for hierarchical buckets).

* Archived, Cold Archive, and Deep Cold Archive objects must be restored before calling rename_object.

* Concurrent calls to rename_object on the same object are not supported.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, but IAM users have no permissions by default. If you need to perform the rename_object operation using a sub\-account, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:RenameObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="basic-object-renaming"></span>
### Basic object renaming

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
use ve_tos_rust_sdk::object::RenameObjectInput;
use ve_tos_rust_sdk::bucket::{PutBucketRenameInput, DeleteBucketRenameInput};
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

    // Define parameters
    let bucket = "example-bucket";
    let old_key = "old-object.txt";
    let new_key = "new-object.txt";

    // Step 1: Enable bucket rename feature (required for flat buckets)
    println!("Enabling bucket rename feature...");
    let put_rename_input = PutBucketRenameInput::new(bucket, true);
    let put_result = client.put_bucket_rename(&put_rename_input).await;
    match put_result {
        Ok(output) => {
            println!("Bucket rename feature enabled successfully. Request ID: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error when enabling bucket rename: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error when enabling bucket rename: Request ID: {}, EC: {}, Code: {}", request_id, ec, code);
                }
                _ => println!("Unexpected error when enabling bucket rename: {:?}", err),
            }
            return;
        }
    }

    // Wait for feature propagation
    println!("Waiting for bucket rename feature to take effect...");
    tokio::time::sleep(Duration::from_secs(10)).await;

    // Step 2: Perform basic object rename
    println!("Performing basic object rename...");
    let input = RenameObjectInput::new(bucket, old_key, new_key);
    let rename_result = client.rename_object(&input).await;
    match rename_result {
        Ok(output) => {
            println!("Object renamed successfully. Request ID: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error when renaming object: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error when renaming object: Request ID: {}, EC: {}, Code: {}", request_id, ec, code);
                }
                _ => println!("Unexpected error when renaming object: {:?}", err),
            }
        }
    }

    // Step3: Cleanup - Disable bucket rename feature
    println!("Disabling bucket rename feature...");
    let delete_rename_input = DeleteBucketRenameInput::new(bucket);
    let delete_result = client.delete_bucket_rename(&delete_rename_input).await;
    match delete_result {
        Ok(output) => {
            println!("Bucket rename feature disabled successfully. Request ID: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error when disabling bucket rename: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error when disabling bucket rename: Request ID: {}, EC: {}, Code: {}", request_id, ec, code);
                }
                _ => println!("Unexpected error when disabling bucket rename: {:?}", err),
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation about RenameObject, see [RenameObject](https://docs.byteplus.com/docs/tos/Renameobject).
