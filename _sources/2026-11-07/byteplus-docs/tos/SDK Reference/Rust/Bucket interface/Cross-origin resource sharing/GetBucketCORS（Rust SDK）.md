---
title: "GetBucketCORS（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketCORS"
---

The get_bucket_cors interface retrieves the cross\-origin resource sharing (CORS) configuration rules of a bucket. This article explains how to use the get_bucket_cors interface in the Rust SDK to read these rules.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code in this article reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has full permissions by default, but IAM users have no permissions by default. If you want to use a sub\-account to perform get_bucket_cors operations, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketCORS

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="9bf92246"></span>
### Retrieve the CORS configuration for a specified bucket

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
use ve_tos_rust_sdk::bucket::GetBucketCORSInput;
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

    // Failure to obtain CORS configuration (e.g., insufficient permissions)
    let bucket_name = "no-permission-bucket";
    let input = GetBucketCORSInput::new(bucket_name);
    let output = client.get_bucket_cors(&input).await;

    match output {
        Ok(_) => println!("Unexpectedly, the CORS configuration of the unauthorized storage bucket was successfully obtained."),
        Err(err) => {
            match err {
                TosError::TosServerError { ec, .. } if ec == "AccessDenied" => println!("Insufficient permissions, failed to obtain CORS configuration."),
                _ => println!("Failed to obtain CORS configuration: {:?}", err),
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation about GetBucketCORS, see [GetBucketCORS](https://docs.byteplus.com/docs/tos/reference-getbucketcors).
