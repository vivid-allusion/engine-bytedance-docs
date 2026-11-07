---
title: "DeleteBucketPolicy（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucketPolicy"
---

The delete_bucket_policy API removes the bucket’s authorization policy. This article explains how to use Rust SDK’s delete_bucket_policy API to remove a specified bucket policy.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The operation returns 204 No Content on success.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If a sub\-account needs to perform the delete_bucket_policy operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteBucketPolicy

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yig6Zmk5oyH5a6a5a2Y5YKo5qG255qE562W55Wl"></span>
### Delete the policy of the specified bucket

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
use ve_tos_rust_sdk::bucket::DeleteBucketPolicyInput;
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

    let bucket_name = "your-bucket-name";
    let delete_input = DeleteBucketPolicyInput::new(bucket_name);
    let delete_output = client.delete_bucket_policy(&delete_input).await;

    match delete_output {
        Ok(output) => {
            println!("Delete the bucket policy successfully，request_id: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, status_code, .. } => {
                    println!("Server error: request_id={}, ec={}, status_code={}", request_id, ec, status_code);
                }
            }
        }
    }
}

```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of DeleteBucketPolicy, see [DeleteBucketPolicy](https://docs.byteplus.com/docs/tos/reference-deletebucketpolicy).
