---
title: "PutBucketRealTimeLog（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketRealTimeLog_Rust_SDK"
---

The put_bucket_real_time_log API enables real\-time log analysis for buckets. This article explains how to configure TLS log collection, role authorization, and retention periods using the put_bucket_real_time_log API in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the example code based on your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the example code reads the Access Key ID and Secret Access Key from environment variables. Before using the SDK, configure long\-term access credentials. For details, see [configuring long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* `use_service_topic` only supports `true`; passing other values will cause the request to fail.

* `ttl` ranges from 0 to 3650; values outside this range will return a parameter error.

* `role` must be set to `TOSLogArchiveTLSRole`; using another role name will trigger configuration denial.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to perform the put_bucket_real_time_log operation using a sub\-account, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutBucketRealTimeLog

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6K6-572u5a2Y5YKo5qG25a6e5pe25pel5b-X6YWN572u"></span>
### Set up the bucket real\-time log configuration

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
use ve_tos_rust_sdk::bucket::{PutBucketRealTimeLogInput, RealTimeLogConfiguration, AccessLogConfiguration};
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

    // Configure real-time logs for the storage bucket.
    let mut access_log_config = AccessLogConfiguration::new();
    access_log_config.set_use_service_topic(true);
    access_log_config.set_tls_project_id("your-tls-project-id");
    access_log_config.set_tls_topic_id("your-tls-topic-id");
    access_log_config.set_tls_dashboard_id("your-tls-dashboard-id");
    access_log_config.set_ttl(7); // Logs are kept for 7 days

    let real_time_log_config = RealTimeLogConfiguration::new("your-role", access_log_config);
    let input = PutBucketRealTimeLogInput::new("example-bucket", real_time_log_config);

    let output = client.put_bucket_real_time_log(&input).await;
    match output {
        Ok(output) => {
            println!("Real-time log configuration successful, request_id: {}", output.request_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
                _ => println!("Unknown error: {:?}", err),
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of PutBucketRealTimeLog, see [PutBucketRealTimeLog](https://docs.byteplus.com/docs/tos/PutBucketRealTimeLog).
