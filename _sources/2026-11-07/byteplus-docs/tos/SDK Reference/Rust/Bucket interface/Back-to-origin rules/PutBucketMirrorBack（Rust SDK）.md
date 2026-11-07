---
title: "PutBucketMirrorBack（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketMirrorBack"
---

The PutBucketMirrorBack interface configures origin rules for a bucket, supporting up to 20 mirror or redirect rules based on conditions. This article explains how to complete this configuration using the PutBucketMirrorBack interface of the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you must configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Only the bucket owner can call this interface to set origin rules.

* A single bucket supports up to 20 origin rules.

* When using private bucket back\-to\-origin, only one authentication method, either Role authentication or AK/SK authentication, can be enabled, not both simultaneously.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have none by default. If you need to use a sub\-account to perform the `PutBucketMirrorBack `operation, the BytePlus main account must grant the following permissions to that sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5): `tos:PutBucketMirrorBack`.

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6YWN572u5a2Y5YKo5qG255qE5Zue5rqQ6KeE5YiZ"></span>
### Configure the bucket's back\-to\-origin rules

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
use ve_tos_rust_sdk::bucket::{PutBucketMirrorBackInput, MirrorBackRule, Condition, Redirect, PublicSource, SourceEndpoint};
use ve_tos_rust_sdk::enumeration::RedirectType;
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
    let mut input = PutBucketMirrorBackInput::new(bucket_name);

    // Create public source rule
    let mut rule = MirrorBackRule::new("rule1");
    let mut condition = Condition::default();
    condition.set_http_code(404);
    condition.set_key_prefix("prefix1");
    condition.set_http_method(vec!["GET".to_string(), "HEAD".to_string()]);
    rule.set_condition(condition);

    let mut redirect = Redirect::default();
    redirect.set_redirect_type(RedirectType::RedirectMirror);
    let public_source = PublicSource::new(SourceEndpoint::new(vec!["http://public-source.example.com".to_string()]));
    redirect.set_public_source(public_source);
    rule.set_redirect(redirect);

    input.add_rule(rule);

    let output = client.put_bucket_mirror_back(&input).await;
    match output {
        Ok(output) => println!("Public source mirror back rule configured successfully, request_id: {}", output.request_id()),
        Err(err) => match err {
            TosError::TosClientError { message, .. } => println!("Client error: {}", message),
            TosError::TosServerError { request_id, ec, .. } => println!("Server error: request_id: {}, ec: {}", request_id, ec),
        },
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on PutBucketMirrorBack, see [PutBucketMirrorBack](https://docs.byteplus.com/docs/tos/Putbucketmirrorback).
