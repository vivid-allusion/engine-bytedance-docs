---
title: "DeleteBucketRename（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucketRename"
---

The delete_bucket_rename interface disables the RenameObject feature for a bucket. This article explains how to disable this feature using the delete_bucket_rename interface in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code based on your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Before calling, ensure the bucket has enabled the RenameObject feature; otherwise, you will receive a 404 NoSuchBucketRenameConfiguration error.

* This operation takes effect immediately. After it takes effect, you cannot revert it through the same API and must call put_bucket_rename to enable it again.

* A 200 response only indicates the interface call succeeded; it does not guarantee that metadata of renamed objects in the bucket will automatically roll back.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has full permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the delete_bucket_rename operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteBucketRename

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yig6Zmk5a2Y5YKo5qG255qE6YeN5ZG95ZCN5Yqf6IO9"></span>
### Delete the bucket rename function

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
use ve_tos_rust_sdk::bucket::DeleteBucketRenameInput;
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

    let bucket = "example-bucket";
    let input = DeleteBucketRenameInput::new(bucket);
    let output = client.delete_bucket_rename(&input).await;
    match output {
        Ok(_) => println!("Successfully deleted bucket rename feature for bucket: {}", bucket),
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code),
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of DeleteBucketRename, see [DeleteBucketRename](https://docs.byteplus.com/docs/tos/Deletebucketrename).
