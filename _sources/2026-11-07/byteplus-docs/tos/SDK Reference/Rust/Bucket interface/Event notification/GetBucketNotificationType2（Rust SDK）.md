---
title: "GetBucketNotificationType2（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketNotificationType2"
---

The get_bucket_notification_type2 interface retrieves the event notification rules of a bucket. This article explains how to use the Rust SDK's get_bucket_notification_type2 interface to read the configured rule list.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you must configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Tiered buckets do not support the get_bucket_notification_type2 interface.

* The returned `rules` contain up to 5 destinations.

* If `rule_id` is not set, TOS automatically generates a name up to 255 characters.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus primary account has all permissions by default, but IAM users do not have any permissions by default. If a sub\-account needs to perform the get_bucket_notification_type2 operation, the BytePlus primary account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketNotificationType2

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6I635Y-W5a2Y5YKo5qG255qE6YCa55-l6YWN572u"></span>
### Retrieve the notification configuration of a bucket

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
use ve_tos_rust_sdk::bucket::GetBucketNotificationType2Input;

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

    // Create input
    let input = GetBucketNotificationType2Input::new("example-bucket");
    
    // Call the API to retrieve notification configuration
    let output = client.get_bucket_notification_type2(&input).await;
    match output {
        Ok(output) => {
            println!("Notification configuration successful，request_id: {}", output.request_id());
            println!("Number of rules: {}", output.rules().len());
            for rule in output.rules() {
                println!("Rules ID: {}", rule.rule_id());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of GetBucketNotificationType2, see [GetBucketNotificationV2](https://docs.byteplus.com/docs/tos/GetBucketNotificationV2).
