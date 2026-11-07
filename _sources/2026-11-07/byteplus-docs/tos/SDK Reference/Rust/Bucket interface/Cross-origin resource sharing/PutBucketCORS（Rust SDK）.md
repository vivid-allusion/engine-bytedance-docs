---
title: "PutBucketCORS（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketCORS"
---

The put_bucket_cors interface sets CORS rules for a bucket. This article explains how to configure cross\-origin access using the put_bucket_cors interface in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Before using the SDK, you need to configure long\-term access credentials. For details, see [Configuring long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The total size of all CORS rules must not exceed 20 KiB.

* If `ResponseVary` is set to `true`, the response will carry the `Vary: Origin` header, which may increase browsing or origin requests.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the put_bucket_cors operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutBucketCORS

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="91070a31"></span>
### Set CORS rules for the bucket

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
use ve_tos_rust_sdk::bucket::{CORSRule, PutBucketCORSInput};

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

    // Configure CORS rules for a single bucket
    let bucket_name = "my-single-bucket";
    let mut rule = CORSRule::new();
    rule.set_allowed_origins(vec!["*".to_string()]);
    rule.set_allowed_methods(vec!["PUT".to_string(), "GET".to_string()]);
    rule.set_allowed_headers(vec!["Authorization".to_string()]);
    rule.set_expose_headers(vec!["x-tos-request-id".to_string()]);
    rule.set_max_age_seconds(1024);
    rule.set_response_vary(true);

    let input = PutBucketCORSInput::new_with_rules(bucket_name, vec![rule]);
    let output = client.put_bucket_cors(&input).await;

    match output {
        Ok(_) => println!("Successfully set CORS rules for bucket: {}", bucket_name),
        Err(err) => eprintln!("Failed to set CORS rules: {:?}", err),
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on PutBucketCORS, see [PutBucketCORS](https://docs.byteplus.com/docs/tos/reference-putbucketcors).
