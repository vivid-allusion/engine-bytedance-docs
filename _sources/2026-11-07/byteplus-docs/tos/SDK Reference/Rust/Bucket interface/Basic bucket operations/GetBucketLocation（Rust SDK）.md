---
title: "GetBucketLocation（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketLocation"
---

The get_bucket_location interface queries the bucket's region information and returns the Region, public network domain, and private network domain. This article explains how to use the Rust SDK's get_bucket_location interface to obtain the bucket's region.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The `Region`, `ExtranetEndpoint`, and `IntranetEndpoint` fields in the response are tightly bound to the region configured when creating the bucket and do not change with requests.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need a sub\-account to perform the get_bucket_location operation, the Volcengine main account must grant the sub\-account the following permissions through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketLocation

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="db03ebc0"></span>
### Query the region information of the specified bucket

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
use ve_tos_rust_sdk::bucket::GetBucketLocationInput;

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

    // Load credentials from environment variables
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let bucket_name = "your-bucket-name";

    // Build TOS client
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().expect("Failed to build TOS client");

    // Create GetBucketLocation input
    let input = GetBucketLocationInput::new(bucket_name);

    // Call GetBucketLocation API
    match client.get_bucket_location(&input).await {
        Ok(output) => {
            println!("Bucket region: {}", output.region());
        }
        Err(err) => {
            eprintln!("Failed to get bucket location: {:?}", err);
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of GetBucketLocation, see [GetBucketLocation](https://docs.byteplus.com/docs/tos/reference-getbucketlocation).
