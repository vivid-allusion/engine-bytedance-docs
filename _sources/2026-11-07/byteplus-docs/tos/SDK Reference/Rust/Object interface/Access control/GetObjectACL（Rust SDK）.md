---
title: "GetObjectACL（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetObjectACL"
---

The get_object_acl interface is used to obtain the access control list (ACL) of an object, supporting specified versions. This article explains how to query ACL information using the Rust SDK's get_object_acl interface.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your situation. For details, see [Region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* If the request includes the `version_id` parameter, it returns the ACL information for that specific `version_id`; otherwise, it defaults to returning the ACL information of the current version.


<span id="f34b5c43"></span>
## Permissions required

The main account of BytePlus has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the get_object_acl operation, the BytePlus main account must grant the following permissions to this sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetObjectACL

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6I635Y-W5oyH5a6a5a-56LGh55qELWFjbA=="></span>
### Get the ACL of the specified object

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
use ve_tos_rust_sdk::object::{GetObjectACLInput, GetObjectACLOutput};
use ve_tos_rust_sdk::common::{Owner, Grant, Grantee};
use ve_tos_rust_sdk::enumeration::{GranteeType, CannedType, PermissionType};
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
    // Initialize tracing log
    let _guard = init_tracing_log("info", "temp/logs", "app.log");

    // Get credentials from environment variables
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";

    // Build TOS client
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    // Case: Get ACL of specified object
    let bucket = "example-bucket-2";
    let key = "example-object";
    let input = GetObjectACLInput::new(bucket, key);

    let output = client.get_object_acl(&input).await;
    match output {
        Ok(output) => {
            println!("version_id: {}", output.version_id());
            println!("owner.id: {}", output.owner().id());
            println!("bucket_owner_entrusted: {}", output.bucket_owner_entrusted());
            println!("is_default: {}", output.is_default());
            println!("grants count: {}", output.grants().len());
            for (index, grant) in output.grants().iter().enumerate() {
                println!("[{}] grant:", index);
                let grantee = grant.grantee();
                println!("  grantee.type: {}", grantee.grantee_type().as_str());
                if let Some(canned) = grantee.canned() {
                    println!("  grantee.canned: {}", canned.as_str());
                }
                if !grantee.id().is_empty() {
                    println!("  grantee.id: {}", grantee.id());
                }
                println!("  permission: {}", grant.permission().as_str());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error message: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
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

For the API documentation of GetObjectACL, see [GetObjectACL](https://docs.byteplus.com/docs/tos/reference-getobjectacl).
