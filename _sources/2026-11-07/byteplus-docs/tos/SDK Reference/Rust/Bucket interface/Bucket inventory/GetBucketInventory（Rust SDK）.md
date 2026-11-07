---
title: "GetBucketInventory（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketInventory_Rust_SDK"
---

The get_bucket_inventory interface lets you view the specified inventory rule in a bucket. This article explains how to retrieve the rule configuration using the get_bucket_inventory interface in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, this sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you must configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The query parameters `inventory` and `id` must be provided together; if either is missing, a 400 error will be returned.

* If the target bucket is not granted the corresponding role’s read/write permissions, the interface returns 403 and fails to retrieve the inventory configuration.

* Inventory files only support CSV format compressed with GZIP; requests using other formats will be rejected.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the get_bucket_inventory operation, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketInventory

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="deab6a15"></span>
### Retrieve inventory rules for the specified bucket

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
use ve_tos_rust_sdk::bucket::GetBucketInventoryInput;
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

    // Case: Get specified bucket inventory rule
    let input = GetBucketInventoryInput::new("example-bucket", "existing-id");
    let output = client.get_bucket_inventory(&input).await;
    match output {
        Ok(output) => {
            println!("id: {}", output.id());
            println!("is_enabled: {}", output.is_enabled());
            if let Some(filter) = output.filter() {
                println!("filter.prefix: {}", filter.prefix());
            }
            if let Some(destination) = output.destination() {
                if let Some(tos_dst) = destination.tos_bucket_destination() {
                    println!("destination.tos_bucket_destination.format: {}", tos_dst.format().as_str());
                    println!("destination.tos_bucket_destination.account_id: {}", tos_dst.account_id());
                    println!("destination.tos_bucket_destination.role: {}", tos_dst.role());
                    println!("destination.tos_bucket_destination.bucket: {}", tos_dst.bucket());
                    println!("destination.tos_bucket_destination.prefix: {}", tos_dst.prefix());
                }
            }
            if let Some(schedule) = output.schedule() {
                println!("schedule.frequency: {}", schedule.frequency().as_str());
            }
            println!("included_object_versions: {}", output.included_object_versions().as_str());
            if let Some(opt_fields) = output.optional_fields() {
                println!("optional_fields.field count: {}", opt_fields.field().len());
                for (idx, field) in opt_fields.field().iter().enumerate() {
                    println!("optional_fields.field[{}]: {}", idx, field);
                }
            }
            println!("is_un_compressed: {}", output.is_un_compressed());
        }
        Err(err) => handle_error(err),
    }
}

fn handle_error(err: TosError) {
    match err {
        TosError::TosClientError { message, .. } => {
            println!("Client error: {}", message);
        }
        TosError::TosServerError { request_id, ec, code, .. } => {
            println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
        }
        _ => println!("Unknown error: {:?}", err),
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the GetBucketInventory API documentation, see [GetBucketInventory](https://docs.byteplus.com/docs/tos/GetBucketInventory).
