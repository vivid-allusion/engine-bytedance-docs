---
title: "PutBucketNotificationType2（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketNotificationType2"
---

The put_bucket_notification_type2 API configures event notification rules for buckets. This article explains how to use the Rust SDK's put_bucket_notification_type2 API to set rules that push object creation or deletion events to VeFaaS or Kafka.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you must configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Put_bucket_notification_type2 API is not supported for tiered buckets.

* Rule IDs within the same bucket must be unique and can have a maximum length of 255 characters.

* `destination` must contain at least 1 and no more than 5 different targets.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the put_bucket_notification_type2 operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutBucketNotificationType2

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6K6-572u6YCa55-l6KeE5YiZ55qE55uu5qCH5Li6LXZlZmFhcy3lh73mlbA="></span>
### Set the notification rule target to a VeFaaS function

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
use ve_tos_rust_sdk::bucket::{PutBucketNotificationType2Input, NotificationRule, NotificationDestination, DestinationVeFaaS};
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

    // Create notification rules
    let mut rule = NotificationRule::new("vefaas-notify-rule");
    rule.set_events(vec!["tos:ObjectRemoved:Delete".to_string()]);

    // Set VeFaaS function target
    let mut destination = NotificationDestination::new();
    destination.set_ve_faas(vec![DestinationVeFaaS::new("vefaas-function-123")]);

    rule.set_destination(destination);

    // Create input
    let input = PutBucketNotificationType2Input::new("example-bucket", vec![rule]);

    // Call the API to set notification configuration
    let output = client.put_bucket_notification_type2(&input).await;
    match output {
        Ok(output) => {
            println!("VeFaaS target notification rule set successfully，request_id: {}", output.request_id());
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

For the API documentation of PutBucketNotificationType2, see [PutBucketNotificationV2](https://docs.byteplus.com/docs/tos/PutBucketNotificationV2).
