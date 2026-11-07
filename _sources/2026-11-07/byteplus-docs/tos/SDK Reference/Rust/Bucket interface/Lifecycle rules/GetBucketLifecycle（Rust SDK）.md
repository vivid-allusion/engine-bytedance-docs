---
title: "GetBucketLifecycle（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketLifecycle"
---

The get_bucket_lifecycle interface retrieves the bucket lifecycle rules, supporting configurations based on last modified time or last accessed time. This article explains how to query rule details through the Rust SDK's get_bucket_lifecycle interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Region and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, this example code reads the Access Key ID and Secret Access Key from environment variables. Before using the SDK, you must configure permanent access credentials. For details, see [Configuring long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* When Bucket versioning is enabled, the response fields `Expiration` and `Transitions` apply to the current version, while `NoncurrentVersionExpiration` and `NoncurrentVersionTransitions` apply to previous versions.

* If a rule configures both `Days` and `Date`, TOS prioritizes `Date` and ignores `Days`.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the get_bucket_lifecycle operation, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetLifecycleConfiguration

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="e82614a1"></span>
### Retrieve the lifecycle rules of the specified bucket

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
use ve_tos_rust_sdk::bucket::{GetBucketLifecycleInput};
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

    let bucket_name = "my-bucket";
    let input = GetBucketLifecycleInput::new(bucket_name);
    let output = client.get_bucket_lifecycle(&input).await;

    match output {
        Ok(output) => {
            println!("Total lifecycle rules: {}", output.rules().len());
            for (index, rule) in output.rules().iter().enumerate() {
                println!("Rule {}:", index + 1);
                println!("  ID: {}", rule.id());
                println!("  Prefix: {}", rule.prefix());
                println!("  Status: {:?}", rule.status());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error: {}", message),
                TosError::TosServerError { request_id, ec, .. } => println!("Server error: request_id={}, ec={}", request_id, ec),
            }
        }
    }
}
```


&nbsp;

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of GetBucketLifecycle, see [GetBucketLifecycle](https://docs.byteplus.com/docs/tos/reference-getbucketlifecycle).
