---
title: "DeleteBucket（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucket"
---

The delete_bucket interface deletes an already created empty bucket. This article explains how to perform this operation using the Rust SDK's delete_bucket interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your situation. For details, see [Region and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The bucket must be empty; otherwise, deletion will fail.

* The deletion operation is irreversible.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the delete_bucket operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteBucket

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="38859dfc"></span>
### Delete the specified bucket using the default configuration

```Rust
use async_trait::async_trait; 
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use tokio::task::JoinError;
use futures_core::future::BoxFuture;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::DeleteBucketInput;

#[derive(Debug, Default)]
pub struct TokioRuntime {}

#[async_trait]
impl AsyncRuntime for TokioRuntime {
    type JoinError = JoinError;
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
    // Initialize log
    let _guard = init_tracing_log("info", "temp/logs", "app.log");

    // Obtain AK and SK from environment variables
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or_default();
    let sk = env::var("TOS_SECRET_KEY").unwrap_or_default();
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";

    // Build a TOS client
    let client = tos::builder::<TokioRuntime>()
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build()
        .expect("Failed to build TOS client");

    // Specify the bucket name to be deleted
    let bucket_name = "my-test-bucket";
    let input = DeleteBucketInput::new(bucket_name);

    // Call the delete bucket interface
    let result = client.delete_bucket(&input).await;
    match result {
        Ok(output) => println!("Successfully deleted bucket: {}", bucket_name),
        Err(e) => eprintln!("Failed to delete bucket: {:?}", e),
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of DeleteBucket, see [DeleteBucket](https://docs.byteplus.com/docs/tos/reference-deletebucket).
