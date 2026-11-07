---
title: "GetBucketVersioning（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketVersioning"
---

get_bucket_versioning interface is used to get the versioning status of a bucket. This article explains how to query this status through the Rust SDK's get_bucket_versioning interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Tiered buckets do not support the get_bucket_versioning interface; requests will return an error.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need a sub\-account to perform get_bucket_versioning operations, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketVersioning

<span id=".5Luj56CB56S65L6L"></span>
## Code examples

<span id=".6I635Y-W5oyH5a6a5a2Y5YKo5qG255qE54mI5pys5o6n5Yi254q25oCB"></span>
### Retrieve the versioning status of a specified bucket

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
use ve_tos_rust_sdk::bucket::{GetBucketVersioningInput, GetBucketVersioningOutput};
use ve_tos_rust_sdk::enumeration::VersioningStatusType;
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
    // Initialize logging
    let _guard = init_tracing_log("info", "temp/logs", "app.log");
    
    // Get credentials from environment variables
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
    
    // Create input with specified bucket
    let bucket_name = "example-bucket";
    let input = GetBucketVersioningInput::new(bucket_name);
    
    // Call GetBucketVersioning API
    let result = client.get_bucket_versioning(&input).await;
    
    // Handle result
    match result {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            println!("Bucket versioning status: {}", output.status().as_str());
            match output.status() {
                VersioningStatusType::VersioningStatusNotSet => println!("Versioning is not enabled") ,
                VersioningStatusType::VersioningStatusEnabled => println!("Versioning is enabled") ,
                VersioningStatusType::VersioningStatusSuspended => println!("Versioning is suspended") ,
            }
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message) ,
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server error: Request ID: {}, Error Code: {}, HTTP Status: {}", request_id, code, ec) ,
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of GetBucketVersioning, see [GetBucketVersioning](https://docs.byteplus.com/docs/tos/Getbucketversioning).
