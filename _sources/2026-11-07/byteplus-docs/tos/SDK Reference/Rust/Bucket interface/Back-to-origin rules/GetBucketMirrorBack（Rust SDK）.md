---
title: "GetBucketMirrorBack（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketMirrorBack"
---

The get_bucket_mirror_back interface retrieves the Bucket's origin fetching rules. This article explains how to use the get_bucket_mirror_back interface in the Rust SDK to read configured mirror or redirect origin policies.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Region and Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Before using the SDK, configure long\-term access credentials. For details, see [Configure Long-term Access Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Hierarchical buckets do not support calling get_bucket_mirror_back.

* The origin fetching condition only takes effect when the download request returns 404.

* You can configure up to 5 origin addresses, each no longer than 255 characters.

* HTTP headers such as Host, Content\-Length, Date, and Authorization will be automatically filtered out.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users do not have any permissions by default. If you need to perform the get_bucket_mirror_back operation using a subaccount, the BytePlus main account must grant the following permissions to the subaccount through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketMirrorBack

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6I635Y-W5qG255qE5Zue5rqQ6KeE5YiZ"></span>
### Retrieve the bucket's mirroring rules

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
use ve_tos_rust_sdk::bucket::{GetBucketMirrorBackInput};
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
    let input = GetBucketMirrorBackInput::new(bucket_name);
    let result = client.get_bucket_mirror_back(&input).await;

    match result {
        Ok(output) => {
            println!("request_id: {}", output.request_id());
            let rules = output.rules();
            println!("Number of rules: {}", rules.len());
            for (idx, rule) in rules.iter().enumerate() {
                println!("\nRule [{}]:", idx);
                println!("  ID: {}", rule.id());
                let condition = rule.condition();
                println!("  Condition:");
                println!("    HttpCode: {}", condition.http_code());
                println!("    KeyPrefix: {}", condition.key_prefix());
                println!("    KeySuffix: {}", condition.key_suffix());
                println!("    AllowHost: {:?}", condition.allow_host());
                println!("    HttpMethod: {:?}", condition.http_method());
                let redirect = rule.redirect();
                println!("  Redirect:");
                println!("    RedirectType: {}", redirect.redirect_type().as_str());
                println!("    FetchSourceOnRedirect: {}", redirect.fetch_source_on_redirect());
                println!("    PassQuery: {}", redirect.pass_query());
                println!("    FollowRedirect: {}", redirect.follow_redirect());
                if let Some(public_source) = redirect.public_source() {
                    println!("    PublicSource:");
                    let source_endpoint = public_source.source_endpoint();
                    println!("      Primary Endpoints: {:?}", source_endpoint.primary());
                }
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id={}, ec={}, code={}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of GetBucketMirrorBack, refer to [GetBucketMirrorBack](https://docs.byteplus.com/docs/tos/Getbucketmirrorback).
