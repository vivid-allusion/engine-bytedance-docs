---
title: "GetBucketRename（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketRename"
---

The get_bucket_rename interface checks whether the bucket has enabled the RenameObject feature. This article explains how to use the Rust SDK's get_bucket_rename interface to retrieve this configuration status.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code based on your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the example code reads Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* This interface only returns the current bucket's rename switch status and does not return historical configuration records or operation logs.

* If the bucket has not enabled the RenameObject feature, calling RenameObject\-related interfaces returns 403 Forbidden.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, while IAM users have no permissions by default. If you need to perform the get_bucket_rename operation using a sub\-account, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketRename

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5p-l6K-i5oyH5a6a5a2Y5YKo5qG255qE6YeN5ZG95ZCN5Yqf6IO954q25oCB"></span>
### Check the rename status of the specified bucket

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
use ve_tos_rust_sdk::bucket::GetBucketRenameInput;
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
    // Initialization log
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

    // Create a GetBucketRenameInput instance and specify the bucket name.
    let input = GetBucketRenameInput::new("example-bucket");
    
    // Call the get_bucket_rename interface
    let output = client.get_bucket_rename(&input).await;
    
    match output {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            println!("Storage bucket renaming function status: {}", output.rename_enable());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
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

For the API documentation on GetBucketRename, see [GetBucketRename](https://docs.byteplus.com/docs/tos/Getbucketrename).
