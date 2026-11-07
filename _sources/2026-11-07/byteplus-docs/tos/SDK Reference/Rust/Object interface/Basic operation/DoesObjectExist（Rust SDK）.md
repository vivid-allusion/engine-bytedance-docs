---
title: "DoesObjectExist（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DoesObjectExist"
---

The does_object_exist interface checks if a specified object exists in the bucket. This article explains how to use the does_object_exist interface in the Rust SDK to perform existence checks and return a boolean result.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Region and Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code in this article reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure Long-Term Access Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).


<span id="4f8f01e4"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you want to use a sub\-account to perform the does_object_exist operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:HeadObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yik5pat5a-56LGh5piv5ZCm5a2Y5Zyo"></span>
### Check if the object exists

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
use ve_tos_rust_sdk::object::{DoesObjectExistInput};
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
    let existing_key = "test-object.txt";

    // Check if the object exists
    let exists_input = DoesObjectExistInput::new(bucket, existing_key);
    let exists_result = client.does_object_exist(&exists_input).await;
    match exists_result {
        Ok(exists) => println!("Object exists: {}", exists),
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client error checking existence: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server error checking existence: request_id={}, ec={}, code={}", request_id, ec, code),
            }
        }
    }
}

```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of DoesObjectExist, see [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject).
