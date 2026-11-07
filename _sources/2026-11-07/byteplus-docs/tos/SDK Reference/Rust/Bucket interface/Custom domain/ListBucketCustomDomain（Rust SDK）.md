---
title: "ListBucketCustomDomain（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/ListBucketCustomDomain"
---

The list_bucket_custom_domain API retrieves the custom domain configuration list for a specified Bucket. This article explains how to use the list_bucket_custom_domain API in the Rust SDK to query bound domains, certificate status, and disable reasons.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code based on your situation. For details, see [Region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you must configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need a sub\-account to perform the list_bucket_custom_domain operation, the BytePlus main account must grant the following permissions to the sub\-account via [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policy](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:ListBucketCustomDomain

<span id=".5Luj56CB56S65L6L"></span>
## Code examples

<span id=".5YiX5Ye65oyH5a6a5a2Y5YKo5qG255qE6Ieq5a6a5LmJ5Z-f5ZCN"></span>
### List custom domains of the specified bucket

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::sync::Arc;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::ListBucketCustomDomainInput;
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
    // Initialize SDK client
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or_else(|_| "".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or_else(|_| "".to_string());
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
        .build()
        .unwrap();

    // Create request input
    let input = ListBucketCustomDomainInput::new("test-bucket");

    // Calling the interface
    match client.list_bucket_custom_domain(&input).await {
        Ok(output) => {
            println!("Successfully retrieved the list of custom domains");
            for domain in output.rules() {
                println!("Domain name: {}", domain.domain());
                println!("Certificate ID: {}", domain.cert_id());
                println!("Certificate status: {}", domain.cert_status());
                println!("Protocol type: {}", domain.protocol());
                println!("Disabled: {}", domain.forbidden());
                println!("Reasons for disabling: {}", domain.forbidden_reason());
            }
        }
        Err(err) => {
            eprintln!("Failed to retrieve list of custom domains: {:?}", err);
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of ListBucketCustomDomain, see [GetBucketCustomDomain](https://docs.byteplus.com/docs/tos/Getbucketcustomdomain).
