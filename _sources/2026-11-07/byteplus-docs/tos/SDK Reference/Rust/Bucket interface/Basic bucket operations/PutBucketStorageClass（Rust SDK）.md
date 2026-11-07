---
title: "PutBucketStorageClass（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketStorageClass"
---

The put_bucket_storage_class interface sets the default storage class for a bucket. This article explains how to use the Rust SDK's put_bucket_storage_class interface to complete this configuration.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the example code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, configure the long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The TOS SDK supports temporary access credentials and allows flexible settings such as timeout and retry policies to improve application security according to business needs.

* Cold Archive and Deep Cold Archive types are available only in China (Beijing), China (Shanghai), and China (Guangzhou) regions. Deep Cold Archive requires an additional invitation application.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the put_bucket_storage_class operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutBucketStorageClass

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="3cbdf25f"></span>
### Set the storage type of the bucket to Infrequent Access storage

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
use ve_tos_rust_sdk::bucket::PutBucketStorageClassInput;
use ve_tos_rust_sdk::enumeration::StorageClassType;
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
    // initialize log
    let _guard = init_tracing_log("info", "temp/logs", "app.log");

    // get AK/SK from environment variables
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com"; // sample endpoint, modify according to actual conditions
    let region = "cn-beijing"; // sample region, modify according to actual conditions

    // Build TOS client
    let client = tos::builder::<TokioRuntime>()
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build()
        .expect("Client build failed");

    // Bucket name, replace with the actual bucket name
    let bucket_name = "example-bucket";

    // Create input for setting bucket storage class (Infrequent Access Storage)
    let input = PutBucketStorageClassInput::new_with_storage_class(
        bucket_name,
        StorageClassType::StorageClassIa,
    );

    // Call put_bucket_storage_class interface
    match client.put_bucket_storage_class(&input).await {
        Ok(output) => {
            println!("Bucket storage type set successfully，Request ID: {}", output.request_id());
        }
        Err(err) => {
            eprintln!("Failed to set bucket storage type: {:?}", err);
            match err {
                TosError::TosClientError { message, .. } => {
                    eprintln!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, message, .. } => {
                    eprintln!("Server error - Request ID: {}, Error code: {}, Message: {}", request_id, ec, message);
                }
                _ => {
                    eprintln!("Unknown error: {:?}", err);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of PutBucketStorageClass, see [PutBucketStorageClass](https://docs.byteplus.com/docs/tos/reference-putbucketstorageclass).
