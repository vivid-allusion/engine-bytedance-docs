---
title: "GetBucketEncryption（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketEncryption"
---

The get_bucket_encryption API retrieves the server\-side encryption configuration of a bucket. This article explains how to use the Rust SDK's get_bucket_encryption API to read SSE rules.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the example code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The get_bucket_encryption call must use HTTPS protocol.

* Tiered buckets do not support the get_bucket_encryption API.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the get_bucket_encryption operation, the Volcengine main account must grant the sub\-account the following permissions through [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policy](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketEncryption

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6I635Y-W5oyH5a6a5a2Y5YKo5qG255qE5Yqg5a-G6YWN572u"></span>
### Retrieve the encryption configuration of the specified bucket

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
use ve_tos_rust_sdk::bucket::GetBucketEncryptionInput;
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

    let bucket_name = "example-bucket";
    let input = GetBucketEncryptionInput::new(bucket_name);
    let output = client.get_bucket_encryption(&input).await;

    match output {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            let rule = output.rule();
            let sse_config = rule.apply_server_side_encryption_by_default();
            println!("SSE Algorithm: {}", sse_config.sse_algorithm());
            if !sse_config.kms_master_key_id().is_empty() {
                println!("KMS Master Key ID: {}", sse_config.kms_master_key_id());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client Error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, status_code, .. } => {
                    println!("Server Error - Request ID: {}, Code: {}, Status Code: {}, EC: {}", request_id, code, status_code, ec);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of GetBucketEncryption, see [GetBucketEncryption](https://docs.byteplus.com/docs/tos/Getbucketencryption).
