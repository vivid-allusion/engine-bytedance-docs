---
title: "PutBucketLifecycle（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketLifecycle"
---

The put_bucket_lifecycle interface sets lifecycle rules for a bucket. This article explains how to use the put_bucket_lifecycle interface in the Rust SDK to automatically transition or delete objects.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain name in the sample code based on your actual situation. For detailed information, see [Region and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code in this article reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For detailed information, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The maximum number of lifecycle rules permitted for a bucket is 1,000. Additionally, each bucket enforces a 20 KB cumulative limit for all JSON\-formatted lifecycle policies.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the put_bucket_lifecycle operation, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutLifecycleConfiguration

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="1c41a884"></span>
### Set a single lifecycle rule for the bucket

```Rust
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::{init_tracing_log, Tag};
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::{PutBucketLifecycleInput, LifecycleRule, Expiration, Transition};
use ve_tos_rust_sdk::enumeration::{StatusType, StorageClassType};
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

    // Set a single lifecycle rule: logs/prefix objects expire after 30 days.
    let bucket_name = "example-bucket";
    let mut rule = LifecycleRule::new("expire-logs-rule".to_string());
    rule.set_prefix("logs/".to_string());
    rule.set_status(StatusType::StatusEnabled);
    rule.set_expiration(Expiration::new_with_days(30isize));
    let mut transitions = Vec::new();
    let mut transition = Transition::new(StorageClassType::StorageClassIa);
    transition.set_days(10isize);
    transitions.push(transition);
    rule.set_transitions(transitions);
    let mut tags = Vec::new();
    let tag = Tag::new("key", "value");
    tags.push(tag);
    rule.set_tags(tags);
    let input = PutBucketLifecycleInput::new_with_rules(bucket_name, vec![rule]);

    match client.put_bucket_lifecycle(&input).await {
        Ok(output) => println!("Success: Request ID = {}", output.request_id()),
        Err(err) => match err {
            TosError::TosClientError { message, .. } => println!("Client Error: {}", message),
            TosError::TosServerError { request_id, ec, code,.. } => println!("Server Error: Request ID = {}, EC={} ,Code = {}", request_id, ec, code)
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of PutBucketLifecycle, see [PutBucketLifecycle](https://docs.byteplus.com/docs/tos/reference-putbucketlifecycle).
