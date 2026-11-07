---
title: "PutObjectTagging（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutObjectTagging"
---

The put_object_tagging interface sets or overwrites tags on an object and supports version control. This article explains how to perform this operation using the put_object_tagging interface of the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain name in the sample code according to your situation. For details, see [region and access domain name](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* When calling put_object_tagging, if the object already has tags, the new tags fully overwrite the old ones; if no tags exist, the new tags are written directly.

* Each object supports up to 10 tags, and keys in the tags list must be unique and not duplicated.

* Key and value are case sensitive, with lengths not exceeding 128 and 256 characters respectively.

* When a bucket has versioning enabled and the target version is a delete marker, put_object_tagging returns 404 not found; you can specify a non\-current version with the `version_id` parameter to set tags.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus master account has all permissions by default, while IAM users have no permissions by default. If you need to perform put_object_tagging using a sub\-account, the BytePlus master account must grant the sub\-account the following permissions through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutObjectTagging

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6K6-572u5a-56LGh5qCH562-"></span>
### Setting tags for an object

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::PutObjectTaggingInput;
use ve_tos_rust_sdk::common::TagSet;
use ve_tos_rust_sdk::common::Tag;
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

    let bucket_name = "example-bucket-2";
    let object_key = "example-object.txt";
    let mut input = PutObjectTaggingInput::new(bucket_name, object_key);
    input.set_tag_set(TagSet::new(vec![
        Tag::new("project", "rust-sdk-demo"),
        Tag::new("env", "test")
    ]));

    let output = client.put_object_tagging(&input).await;
    match output {
        Ok(res) => {
            println!("Successfully set tags for object. Request ID: {}", res.request_id());
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: Request ID: {}, EC: {}, Code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of PutObjectTagging, see [PutObjectTagging](https://docs.byteplus.com/docs/tos/reference-putobjecttagging-).
