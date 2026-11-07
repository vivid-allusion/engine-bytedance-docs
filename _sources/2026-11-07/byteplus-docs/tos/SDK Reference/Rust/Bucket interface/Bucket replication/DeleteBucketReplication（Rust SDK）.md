---
title: "DeleteBucketReplication（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucketReplication"
---

The delete_bucket_replication interface deletes cross\-region or same\-region replication rules for a bucket. This article explains how to perform this operation using Rust SDK's delete_bucket_replication interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain name in the sample code according to your actual situation. For details, see [region and access domain name](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Before using the SDK, configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Get_bucket_replication interface is not supported for tiered buckets.

* Deletion is irreversible; please ensure the rules are backed up.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the delete_bucket_replication operation, the Volcengine main account must grant the sub\-account the following permissions through [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policy](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteBucketReplication

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yig6Zmk5a2Y5YKo5qG25aSN5Yi26KeE5YiZ"></span>
### Delete bucket replication rule

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
use ve_tos_rust_sdk::bucket::DeleteBucketReplicationInput;
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
    let region ="cn-beijing";
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    let bucket_name = "test-bucket-replication";
    let input = DeleteBucketReplicationInput::new(bucket_name);

    let output = client.delete_bucket_replication(&input).await;
    match output {
        Ok(_) => println!("Successfully deleted the bucket copy rule"),
        Err(err) => match err {
            TosError::TosClientError { message, .. } => println!("Client error: {}", message),
            TosError::TosServerError { request_id, ec, .. } => println!("Server error - Request ID: {}, Error code: {}", request_id, ec)
        }
    }
}

```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on DeleteBucketReplication, see [DeleteBucketReplication](https://docs.byteplus.com/docs/tos/Deletebucketreplication).
