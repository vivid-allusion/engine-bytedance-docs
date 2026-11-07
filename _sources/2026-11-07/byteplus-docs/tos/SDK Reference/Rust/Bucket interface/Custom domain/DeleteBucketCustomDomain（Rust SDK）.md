---
title: "DeleteBucketCustomDomain（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucketCustomDomain"
---

The delete_bucket_custom_domain API deletes a specific custom domain configuration of a bucket. This article explains how to perform this operation using the delete_bucket_custom_domain API in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Region and Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure Long-Term Access Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The caller must be the bucket owner or have `DeleteBucketCustomDomain` permission.

* The `customdomain` parameter only supports a single domain name and does not support batch deletion.

* If the `customdomain` value does not match any domain bound to the bucket, the API returns 404 NoSuchCustomDomain.

* After successful deletion, the domain will stop resolving to the bucket within 1 minute.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the delete_bucket_custom_domain operation, the BytePlus main account must grant the following permissions to that sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:DeleteBucketCustomDomain

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yig6Zmk5oyH5a6a5a2Y5YKo5qG255qE6Ieq5a6a5LmJ5Z-f5ZCN6YWN572u"></span>
### Delete the custom domain configuration of a specified bucket

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::DeleteBucketCustomDomainInput;

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
    // Initialize the TOS client
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let client = tos::builder::<TokioRuntime>()
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    // Create a request to delete a custom domain
    let input = DeleteBucketCustomDomainInput::new("example-bucket", "example.com");

    // Perform a deletion operation
    match client.delete_bucket_custom_domain(&input).await {
        Ok(output) => {
            println!("Deletion successful. Requesting ID: {}", output.request_id());
            println!("Status code: {}", output.status_code());
        }
        Err(err) => {
            eprintln!("Deletion failed: {:?}", err);
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For API documentation about DeleteBucketCustomDomain, see [DeleteBucketCustomDomain](https://docs.byteplus.com/docs/tos/Deletebucketcustomdomain).
