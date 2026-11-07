---
title: "GetBucketTagging（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketTagging"
---

The get_bucket_tagging interface retrieves the bucket's tag set. This article explains how to read the bucket tag key\-value list using the get_bucket_tagging interface in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* If no tags are set for the bucket, the response returns 200 OK, and `TagSet.Tags` is an empty array.

* The tag key and value must comply with naming rules; otherwise, they will be rejected during setting and no invalid data will be returned when retrieving.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the get_bucket_tagging operation, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketTagging

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6I635Y-W5oyH5a6a5a2Y5YKo5qG255qE5qCH562-5L-h5oGv"></span>
### Retrieve tag information of the specified bucket

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
use ve_tos_rust_sdk::bucket::{GetBucketTaggingInput, GetBucketTaggingOutput};
use ve_tos_rust_sdk::common::{Tag, TagSet};
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
    // Initialize logging
    let _guard = init_tracing_log("info", "temp/logs", "app.log");

    // Load configuration from environment variables
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";

    // Create TOS client
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    // Case: Obtain tag information for a specified storage bucket
    let bucket_name = "example-bucket";
    let input = GetBucketTaggingInput::new(bucket_name);
    let output = client.get_bucket_tagging(&input).await;

    match output {
        Ok(res) => {
            println!("Successfully retrieved bucket tagging information. Request ID: {}", res.request_id());
            let tag_set = res.tag_set();
            println!("Total tags: {}", tag_set.tags().len());
            for (index, tag) in tag_set.tags().iter().enumerate() {
                println!("Tag {}: Key = {}, Value = {}", index + 1, tag.key(), tag.value());
            }
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error occurred: {}", message);
                },
                TosError::TosServerError { request_id, ec, code, status_code, .. } => {
                    println!("Server error: Request ID = {}, Error Code = {}, Status Code = {}", request_id, ec, status_code);
                },
                _ => println!("Unexpected error: {:?}", err),
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of GetBucketTagging, see [GetBucketTagging](https://docs.byteplus.com/docs/tos/Getbuckettagging).
