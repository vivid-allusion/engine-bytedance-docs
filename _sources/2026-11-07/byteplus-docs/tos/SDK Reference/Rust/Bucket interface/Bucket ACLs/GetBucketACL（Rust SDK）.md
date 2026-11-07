---
title: "GetBucketACL（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketACL"
---

The get_bucket_acl interface retrieves the ACL information of a specified bucket. This article explains how to use the Rust SDK's get_bucket_acl interface to read the bucket access control list.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain name in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The caller must have `READ_ACP` permission; otherwise, the request returns 403 Forbidden.

* The `BucketAclDelivered` field in the response only reflects the bucket\-level ACL inheritance switch status and does not indicate the actual current ACL value of the object.

* If the bucket has no custom authorization configured, the Grants array returns only the owner’s `FULL_CONTROL` record.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The main BytePlus account has full permissions by default, but IAM users have no permissions by default. If you need to perform the get_bucket_acl operation using a sub\-account, the main BytePlus account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketACL

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="d746cae4"></span>
### Get access control permissions for a specified bucket

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
use ve_tos_rust_sdk::bucket::GetBucketACLInput;
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
    // Initialization log
    let _guard = init_tracing_log("info", "temp/logs", "app.log");

    // Obtain AK/SK from environment variables
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";

    // Build a TOS client
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    // Use Case 1: Obtain access control permissions for a specified bucket
    let bucket_name = "example-bucket";
    let input = GetBucketACLInput::new(bucket_name);

    let output = client.get_bucket_acl(&input).await;
    match output {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            println!("Bucket Owner ID: {}", output.owner().id());
            println!("ACL inheritance status: {}", output.bucket_acl_delivered());
            println!("Access control permission list:");
            for grant in output.grants() {
                println!("  Type of Authorized Person: {:?}", grant.grantee().grantee_type());
                println!("  Permission: {:?}", grant.permission());
                if let Some(canned) = grant.grantee().canned() {
                    println!("  Predefined groups: {:?}", canned);
                }
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, .. } => {
                    println!("Server error - Request ID: {}, Error code: {}", request_id, ec);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For API documentation of GetBucketACL, see [GetBucketACL](https://docs.byteplus.com/docs/tos/reference-getbucketacl).
