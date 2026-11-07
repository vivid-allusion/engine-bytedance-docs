---
title: "DeleteBucketWebsite（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucketWebsite"
---

The delete_bucket_website interface deletes the website configuration for the specified bucket. This article explains how to delete website configuration using the Rust SDK delete_bucket_website interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The caller must be the bucket owner or have `DeleteBucketWebsite` permission.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has full permissions by default, while IAM users have no permissions by default. If you need to perform the delete_bucket_website operation using a sub\-account, the BytePlus main account must grant the following permissions to that sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteBucketWebsite

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yig6Zmk5oyH5a6aLWJ1Y2tldC3nmoTnvZHnq5nphY3nva4="></span>
### Delete the website configuration of the specified bucket

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
use ve_tos_rust_sdk::bucket::DeleteBucketCORSInput;
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
    // init log
    let _guard = init_tracing_log("info", "temp/logs", "app.log");

    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let bucket = "your-bucket-name";

    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    // Create DeleteBucketCORS input
    let input = DeleteBucketCORSInput::new(bucket);

    // Call delete_bucket_cors API
    let output = client.delete_bucket_cors(&input).await;

    match output {
        Ok(output) => {
            println!("Successfully deleted bucket CORS configuration. Request ID: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, message, .. } => {
                    println!("Server error: Request ID = {}, Error Code = {}, Message = {}", request_id, ec, message);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on DeleteBucketWebsite, see [DeleteBucketWebsite](https://docs.byteplus.com/docs/tos/Deletebucketwebsite).
