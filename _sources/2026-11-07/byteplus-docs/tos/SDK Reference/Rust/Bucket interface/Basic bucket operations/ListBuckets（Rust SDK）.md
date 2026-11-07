---
title: "ListBuckets（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/ListBuckets"
---

The list_buckets interface queries all buckets owned by the current user. This article explains how to use the list_buckets interface in the Rust SDK to get the bucket list, supporting filtering by project or bucket type.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For detailed information, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* If the request header does not carry x\-tos\-project\-name, the returned result includes all buckets the requester has permissions for, regardless of any project.

* When specifying both x\-tos\-project\-name and x\-tos\-bucket\-type, only buckets meeting both the project affiliation and bucket type criteria are returned.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, while IAM users have no permissions by default. If you need to use a sub\-account to perform the list_buckets operation, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:ListBuckets

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="09f7b756"></span>
### Query all bucket information

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
use ve_tos_rust_sdk::bucket::ListBucketsInput;
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
    let client = tos::builder::<TokioRuntime>().ak(ak).sk(sk).region(region).endpoint(endpoint).build().expect("Failed to build client");
    let input = ListBucketsInput::new();
    match client.list_buckets(&input).await {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            println!("Owner ID: {}", output.owner().id());
            output.buckets().iter().for_each(|b| println!("Bucket: {}", b.name()));
        }
        Err(e) => eprintln!("Error: {:?}", e)
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of ListBuckets, see [ListBuckets](https://docs.byteplus.com/docs/tos/reference-listbuckets).
