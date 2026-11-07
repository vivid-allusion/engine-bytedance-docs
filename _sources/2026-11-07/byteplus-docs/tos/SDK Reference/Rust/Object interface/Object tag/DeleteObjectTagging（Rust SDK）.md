---
title: "DeleteObjectTagging（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteObjectTagging"
---

The delete_object_tagging interface is used to delete object tags. This article explains how to delete object tags using the Rust SDK’s delete_object_tagging interface. Supports specifying versionId to delete version tags.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Region and Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure Long-term Access Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* When `version_id` is not provided, delete_object_tagging defaults to operating on the current version.

* If the target version already has a `delete_marker`, delete_object_tagging returns 404 Not Found.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has full permissions by default, but IAM users have no permissions by default. If you need to perform the delete_object_tagging operation using a sub\-account, the BytePlus main account must grant the following permissions to that sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteObjectTagging

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yig6Zmk5oyH5a6a5a-56LGh55qE5qCH562-"></span>
### Delete tags of the specified object

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::object::{DeleteObjectTaggingInput, DeleteObjectTaggingOutput};
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

    let bucket = "example-bucket-2";
    let key = "example-object.txt";
    let input = DeleteObjectTaggingInput::new(bucket, key);
    let output = client.delete_object_tagging(&input).await;

    match output {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                },
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: Request ID: {}, Error Code: {}, Message: {}", request_id, ec, code);
                },
                _ => println!("Unknown error: {:?}", err)
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of DeleteObjectTagging, see [DeleteObjectTagging](https://docs.byteplus.com/docs/tos/reference-deleteobjecttagging).
