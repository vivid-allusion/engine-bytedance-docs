---
title: "RestoreObject（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/RestoreObject"
---

The restore_object API restores Archive, Cold Archive, and Deep Cold Archive objects, and supports extending the temporary copy's validity period. This article explains how to complete the restore operation using the restore_object API in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the example code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the example code in this article reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Soft links do not support restoration and can be accessed directly; if the target file accessed via a soft link is Archive, Cold Archive, or Deep Cold Archive type, you need to restore the target file first.

* After restoring Archive, Cold Archive, and Deep Cold Archive objects, a temporary copy is generated in Standard Storage. The copy’s validity period is specified by the `Days` parameter, ranging from 1 to 365 days, and will be deleted automatically upon expiration.

* Calling restore_object again can extend the copy’s validity period. Extension is supported, but shortening is not.

* The `tier` value of Cold Archive and Deep Cold Archive determines the recovery time.

   * `Expedited`: 1–5 minutes

   * `Standard`: 2–5 hours / 12 hours

   * `Bulk`: 5–12 hours / 48 hours


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus master account has all permissions by default, but IAM users have none by default. To allow a sub\-account to perform the restore_object operation, the BytePlus master account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:RestoreObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5oGi5aSN5b2S5qGj5a-56LGh"></span>
### Restore archived objects

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
use ve_tos_rust_sdk::object::{RestoreObjectInput, RestoreJobParameters};
use ve_tos_rust_sdk::enumeration::TierType;
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

    let bucket_name = "example-bucket";
    let object_key = "archived-object.txt";
    let mut restore_input = RestoreObjectInput::new(bucket_name, object_key);
    restore_input.set_days(7);
    restore_input.set_restore_job_parameters(RestoreJobParameters::new(TierType::TierStandard));

    let result = client.restore_object(&restore_input).await;
    match result {
        Ok(output) => {
            println!("Restore object succeeded. Request ID: {}", output.request_id());
        }
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

For API documentation about RestoreObject, see [RestoreObject](https://docs.byteplus.com/docs/tos/reference-restoreobject).
