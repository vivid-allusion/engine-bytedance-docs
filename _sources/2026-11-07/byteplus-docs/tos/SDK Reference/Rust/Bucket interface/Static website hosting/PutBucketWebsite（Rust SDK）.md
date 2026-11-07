---
title: "PutBucketWebsite（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketWebsite"
---

The put_bucket_website interface configures a Bucket for static website hosting and sets redirect rules. This document explains how to use the put_bucket_website interface in the Rust SDK to complete the configuration.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your situation. For details, see [Region and Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you must configure long\-term access credentials. For details, see [Configure Long-Term Access Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has full permissions by default, but IAM users have no permissions by default. If you need to perform the put_bucket_website operation with a subaccount, the Volcengine main account must grant the following permissions to that subaccount through [IAM Policy](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket Policy](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutBucketWebsite

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6K6-572u572R56uZ6YWN572u6KeE5YiZ"></span>
### Set website configuration rules

```Rust
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::PutBucketWebsiteInput;
use ve_tos_rust_sdk::bucket::IndexDocument;
use ve_tos_rust_sdk::bucket::ErrorDocument;
use ve_tos_rust_sdk::error::TosError;

#[derive(Debug, Default)]
pub struct TokioRuntime {}

#[async_trait::async_trait]
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
        .build().unwrap();

    let bucket = "example-bucket-2";
    let index_doc = IndexDocument::new( "index.html".to_string());
    let error_doc = ErrorDocument::new("error.html".to_string());
    let mut input = PutBucketWebsiteInput::new(bucket);
    input.set_index_document(index_doc);
    input.set_error_document(error_doc);

    let output = client.put_bucket_website(&input).await;
    match output {
        Ok(output) => {
            println!("PutBucketWebsite success, request_id: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id={}, ec={}, code={}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of PutBucketWebsite, see [PutBucketWebsite](https://docs.byteplus.com/docs/tos/Putbucketwebsite).
