---
title: "DeleteBucketInventory（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucketInventory_Rust_SDK"
---

the delete_bucket_inventory interface deletes a specified inventory rule in the bucket. this article explains how to use the delete_bucket_inventory interface in the Rust SDK to perform this operation.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* you need to fill in the region and access domain in the sample code according to your situation. for details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* to prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. therefore, before using the SDK, you must configure long\-term access credentials. for details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* only existing inventory rules can be deleted. if no rule matches the given id, the interface returns 404 Not Found.

* deletion takes effect immediately. on success, it returns 204 No Content with no response body.

* this interface applies only to the specified bucket and does not affect same\-named inventory rules in other buckets.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the delete_bucket_inventory operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteBucketInventory

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yig6Zmk5oyH5a6a5a2Y5YKo5qG255qE5riF5Y2V6KeE5YiZ"></span>
### Delete the inventory rule of a specified bucket

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
use ve_tos_rust_sdk::bucket::{DeleteBucketInventoryInput};
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
    // Initialize tracing log
    let _guard = init_tracing_log("info", "temp/logs", "app.log");

    // Load credentials from environment variables
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";

    // Build TOS client
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    // Case: Delete specified inventory rule of a bucket
    let bucket_name = "example-bucket";
    let inventory_id = "provide your inventory id";
    let input = DeleteBucketInventoryInput::new(bucket_name, inventory_id);

    let result = client.delete_bucket_inventory(&input).await;
    match result {
        Ok(output) => {
            println!("Delete inventory rule successfully, request_id: {}", output.request_id());
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                },
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                },
                _ => {
                    println!("Unknown error: {:?}", err);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of DeleteBucketInventory, see [DeleteBucketInventory](https://docs.byteplus.com/docs/tos/DeleteBucketInventory).
