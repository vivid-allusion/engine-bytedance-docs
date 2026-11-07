---
title: "GetBucketWebsite（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketWebsite"
---

The get_bucket_website interface retrieves the static website configuration of a specified Bucket, including the homepage, error page, and redirect rules. This article explains how to query this configuration using the get_bucket_website interface of the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You must fill in the region and access domain in the sample code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, this article's sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users do not have any permissions by default. If you need to use a sub\-account to perform the get_bucket_website operation, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policy](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketWebsite

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6I635Y-W5oyH5a6a5a2Y5YKo56m66Ze055qE572R56uZ6YWN572u"></span>
### Get the website configuration for the specified storage space

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
use ve_tos_rust_sdk::bucket::GetBucketWebsiteInput;
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
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or_default();
    let sk = env::var("TOS_SECRET_KEY").unwrap_or_default();
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
        .build()
        .unwrap();

    let bucket_name = "my-simple-bucket";
    let input = GetBucketWebsiteInput::new(bucket_name);
    let output = client.get_bucket_website(&input).await;
    match output {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            println!("Index Document: {:?}", output.index_document());
            println!("Error Document: {:?}", output.error_document());
        },
        Err(err) => match err {
            TosError::TosClientError { message, .. } => println!("Client Error: {}", message),
            TosError::TosServerError { request_id, ec, message, .. } => println!("Server Error: RequestID={}, EC={}, Message={}", request_id, ec, message),
        }
    }
}

```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of GetBucketWebsite, see [GetBucketWebsite](https://docs.byteplus.com/docs/tos/Getbucketwebsite).
