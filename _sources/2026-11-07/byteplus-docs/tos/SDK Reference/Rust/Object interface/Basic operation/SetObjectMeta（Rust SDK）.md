---
title: "SetObjectMeta（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/SetObjectMeta"
---

The set_object_meta interface updates metadata of an uploaded object. This article explains how to replace headers such as Cache\-Control, Content\-Type, and x\-tos\-meta\-\* using the Rust SDK's set_object_meta interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, this sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* When calling set_object_meta, any metadata not explicitly provided in the request headers will be deleted, retaining only the values submitted in this request.

* If the target object is stored in Archive, Cold Archive, or Deep Cold Archive storage class, you must complete the restore_object operation before calling set_object_meta.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the set_object_meta operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policy](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5L-u5pS55a-56LGh5YWD5pWw5o2u"></span>
### Modify object metadata

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
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::object::{SetObjectMetaInput};
use chrono::{DateTime, Utc, Duration as ChronoDuration};
use std::collections::HashMap;

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

    // Case: Modify object metadata
    let bucket_name = "example-bucket";
    let object_key = "example-object";

    let mut input = SetObjectMetaInput::new(bucket_name, object_key);

    // Set metadata fields
    input.set_cache_control("no-cache");
    input.set_content_type("application/json");
    let expires_time = Utc::now() + ChronoDuration::hours(1);

    // Set custom metadata
    let mut meta = HashMap::new();
    meta.insert("author".to_string(), "test_user".to_string());
    meta.insert("version".to_string(), "1.0.0".to_string());
    input.set_meta(meta);

    let output = client.set_object_meta(&input).await;

    match output {
        Ok(output) => {
            println!("Set object meta succeeded, request_id: {}", output.request_id());
        }
        Err(err) => {
            match err {
                ve_tos_rust_sdk::error::TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                ve_tos_rust_sdk::error::TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id={}, ec={}, code={}", request_id, ec, code);
                }
                _ => {
                    println!("Unknown error: {:?}", err);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on SetObjectMeta, see [SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta).
