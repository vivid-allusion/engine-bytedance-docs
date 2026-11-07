---
title: "DeleteBucketRealTimeLog（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucketRealTimeLog_Rust_SDK"
---

The delete_bucket_real_time_log interface disables the log analysis feature. This article explains how to disable the log analysis feature using the delete_bucket_real_time_log interface of the Rust SDK. After disabling, the log topic is not deleted automatically and must be cleared manually.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code based on your actual situation. For details, see [Region and Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code in this article reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure Long-term Access Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* After calling delete_bucket_real_time_log, the log topic is not deleted automatically and requires manual cleaning to avoid further charges.

* All buckets in the same region share the same log topic. Deleting it will also remove the historical log records of other buckets in that region.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the delete_bucket_real_time_log operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policy](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteBucketRealTimeLog

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yig6Zmk5oyH5a6a5qG255qE5a6e5pe25pel5b-X6YWN572u"></span>
### Delete the real\-time log configuration of the specified bucket

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
use ve_tos_rust_sdk::bucket::DeleteBucketRealTimeLogInput;
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

    // specify the bucket name of the real-time log configuration to delete
    let bucket_name = "example-bucket";
    let input = DeleteBucketRealTimeLogInput::new(bucket_name);

    // call delete interface
    let result = client.delete_bucket_real_time_log(&input).await;

    match result {
        Ok(output) => {
            println!("Real-time log configuration successfully deleted");
            println!("Request ID: {}", output.request_id());
            println!("Status code: {}", output.status_code());
        }
        Err(err) => {
            println!("Deleting real-time log configuration failed");
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: Request ID={}, Error code={}, Status code={}", request_id, ec, code);
                }
                _ => println!("Unknown error: {:?}", err)
            }
        }
    }
}

```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of DeleteBucketRealTimeLog, see [DeleteBucketRealTimeLog](https://docs.byteplus.com/docs/tos/DeleteBucketRealTimeLog).
