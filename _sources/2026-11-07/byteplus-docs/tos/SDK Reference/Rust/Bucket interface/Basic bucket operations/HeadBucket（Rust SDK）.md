---
title: "HeadBucket（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/HeadBucket"
---

The head_bucket interface checks whether a bucket exists and its access permissions. This article explains how to perform this operation using the Rust SDK's head_bucket interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* If the bucket does not exist or permissions are insufficient, the interface returns 404 Not Found or 403 Forbidden and does not return bucket metadata in the response headers.

* To obtain attributes such as the bucket’s storage class and availability zone redundancy type, the request identity must be authorized and the bucket must exist; otherwise, the corresponding response headers cannot be read.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to perform the head_bucket operation using a sub\-account, the BytePlus main account must grant the sub\-account the following permissions through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:HeadBucket

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="c18d63d0"></span>
### Check whether the bucket exists

```Rust
use async_trait::async_trait; 
use std::env;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::HeadBucketInput;
use ve_tos_rust_sdk::error::TosError;

#[derive(Debug, Default)]
pub struct TokioRuntime {}

#[async_trait]
impl AsyncRuntime for TokioRuntime {
    type JoinError = tokio::task::JoinError;
    async fn sleep(&self, duration: std::time::Duration) {
        tokio::time::sleep(duration).await;
    }

    fn spawn<'a, F>(&self, future: F) -> futures_core::future::BoxFuture<'a, Result<F::Output, Self::JoinError>>
    where
        F: std::future::Future + Send + 'static,
        F::Output: Send + 'static,
    {
        Box::pin(Handle::current().spawn(future))
    }

    fn block_on<F: std::future::Future>(&self, future: F) -> F::Output {
        Handle::current().block_on(future)
    }
}

#[tokio::main]
async fn main() {
    init_tracing_log("info", "temp/logs", "app.log");

    let ak = env::var("TOS_ACCESS_KEY").unwrap_or_default();
    let sk = env::var("TOS_SECRET_KEY").unwrap_or_default();
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let bucket_name = "example-bucket";

    let client = tos::builder::<TokioRuntime>()
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    let input = HeadBucketInput::new(bucket_name);

    let result = client.head_bucket(&input).await;

    match result {
        Ok(output) => {
            println!("Bucket '{}' exists and is accessible.", bucket_name);
            println!("Bucket region: {}", output.region());
            println!("Default storage class: {}", output.storage_class().as_ref().map(|sc| sc.as_str()).unwrap_or("Unknown"));
            println!("AZ redundancy type: {}", output.az_redundancy().as_ref().map(|az| az.as_str()).unwrap_or("Unknown"));
            println!("Bucket type: {}", output.bucket_type().as_ref().map(|bt| bt.as_str()).unwrap_or("flat"));
        }
        Err(err) => {
            match err {
                TosError::TosServerError { status_code, .. } => {
                    if status_code == 404 {
                        println!("Bucket '{}' does not exist.", bucket_name);
                    } else if status_code == 403 {
                        println!("No access permission to bucket '{}'.", bucket_name);
                    } else {
                        println!("Server error: {:?}", err);
                    }
                }
                _ => {
                    println!("Client error: {:?}", err);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on HeadBucket, see [HeadBucket](https://docs.byteplus.com/docs/tos/reference-headbucket).
