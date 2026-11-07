---
title: "DeleteBucketLifecycle（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucketLifecycle"
---

the delete_bucket_lifecycle API deletes bucket lifecycle rules. this article explains how to delete bucket lifecycle rules using the Rust SDK's delete_bucket_lifecycle API.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* you need to fill in the region and access domain in the sample code based on your actual situation. for details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* to prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. therefore, before using the SDK, you must configure long\-term access credentials. for details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* when deleting a non\-existent lifecycle, the API still returns a 204 status code.

* this operation removes all lifecycle rules in the bucket at once and cannot delete them partially.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

the main account of the Volcengine has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the delete_bucket_lifecycle operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteBucketLifecycle

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="fbde9976"></span>
### Delete the bucket lifecycle rules

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
use ve_tos_rust_sdk::bucket::DeleteBucketLifecycleInput;
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
    let bucket = "test-bucket";

    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    // Deleting bucket lifecycle rules
    let delete_input = DeleteBucketLifecycleInput::new(bucket.clone());
    let delete_result = client.delete_bucket_lifecycle(&delete_input).await;

    match delete_result {
        Ok(output) => {
            println!("Lifecycle rule deleted successfully，request_id: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, .. } => {
                    println!("Server error，request_id: {}, Error code: {}", request_id, ec);
                }
            }
        }
    }
}
```


&nbsp;

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of DeleteBucketLifecycle, see [DeleteBucketLifecycle](https://docs.byteplus.com/docs/tos/reference-deletebucketlifecycle).
