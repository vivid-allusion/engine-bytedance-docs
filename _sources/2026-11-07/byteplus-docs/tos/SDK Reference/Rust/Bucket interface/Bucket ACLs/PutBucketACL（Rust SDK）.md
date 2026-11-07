---
title: "PutBucketACL（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketACL"
---

The put_bucket_acl interface sets the bucket's access control permissions, supporting request body or header methods to overwrite the original ACL. This article explains how to complete this operation using the put_bucket_acl interface of Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, refer to [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads Access Key ID and Secret Access Key from environment variables. Before using the SDK, you must configure long\-term access credentials. For details, refer to [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Each call writes up to 100 grants, and the new ACL completely replaces the old ACL.

* When using the `x-tos-acl` header, no other authorization headers can be used.

* If authorized by `x-tos-grant-read-non-list`, you must also carry `x-tos-grant-read-acp`, or the field is invalid.

* Enabling `BucketAclDelivered` requires providing the `Owner` field; otherwise, the configuration will not take effect.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has full permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the put_bucket_acl operation, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutBucketACL

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="33bd0bbd"></span>
### Set object ACL to public read

```Rust
use async_trait::async_trait; 
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::{PutObjectACLInput};
use ve_tos_rust_sdk::enumeration::ACLType;
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

    let bucket = "example-bucket";
    let key = "example-object";
    let input = PutObjectACLInput::new_with_acl(bucket, key, ACLType::ACLPublicRead);
    let output = client.put_object_acl(&input).await;
    match output {
        Ok(_) => println!("Successfully set object ACL to public-read"),
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id="8fbb37ea"></span>
### Set object ACL via the request body

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::{PutObjectACLInput};
use ve_tos_rust_sdk::common::{Owner, Grant, Grantee};
use ve_tos_rust_sdk::enumeration::{GranteeType, PermissionType, CannedType};
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

    let bucket = "example-bucket";
    let key = "example-object";
    let mut input = PutObjectACLInput::new(bucket, key);
    // Replace with actual owner ID
    input.set_owner(Owner::new("your-account-id"));
    let grant = Grant::new(
        Grantee::new_with_canned(GranteeType::GranteeGroup, CannedType::CannedAuthenticatedUsers),
        PermissionType::PermissionRead
    );
    input.set_grants(vec![grant]);
    let output = client.put_object_acl(&input).await;
    match output {
        Ok(_) => println!("Successfully set object ACL via request body"),
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of PutBucketACL, see [PutBucketACL](https://docs.byteplus.com/docs/tos/reference-putbucketacl).
