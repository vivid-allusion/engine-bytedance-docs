---
title: "ListBucketInventory（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/ListBucketInventory_Rust_SDK"
---

The list_bucket_inventory interface is used to batch retrieve all bucket inventory rules in a storage bucket. This article explains how to use the list_bucket_inventory interface in the Rust SDK to accomplish this task.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For more details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code in this article reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For more details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* When `IsTruncated` is `true`, use `NextContinuationToken` as the `continuation-token` parameter in the next request; otherwise, the remaining inventory configurations cannot be retrieved.

* `continuation-token` is only returned if the listing is incomplete. Missing or incorrect values will cause the listing to start over.

* The returned inventory files are always in GZIP\-compressed CSV format; other formats are not supported.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The VolcEngine master account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the list_bucket_inventory operation, the VolcEngine master account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:ListBucketInventory

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="5c523ac5"></span>
### List bucket inventory rules

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
use ve_tos_rust_sdk::bucket::{ListBucketInventoryInput, ListBucketInventoryOutput};
use ve_tos_rust_sdk::error::TosError;
use ve_tos_rust_sdk::bucket::BucketInventoryConfiguration;

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

    let input = ListBucketInventoryInput::new(bucket_name);
    let output = client.list_bucket_inventory(&input).await;

    match output {
        Ok(output) => {
            println!("Is truncated: {}", output.is_truncated());
            println!("Number of configurations: {}", output.configurations().len());

            for (index, config) in output.configurations().iter().enumerate() {
                println!("Configuration [{}]:", index);
                println!("  id: {}", config.id());
                println!("  is_enabled: {}", config.is_enabled());
                if let Some(filter) = config.filter() {
                    println!("  filter prefix: {}", filter.prefix());
                }
                if let Some(dest) = config.destination() {
                    if let Some(tos_dest) = dest.tos_bucket_destination() {
                        println!("  destination bucket: {}", tos_dest.bucket());
                        println!("  destination prefix: {}", tos_dest.prefix());
                    }
                }
                if let Some(schedule) = config.schedule() {
                    println!("  schedule frequency: {}", schedule.frequency().as_str());
                }
                println!("  included object versions: {}", config.included_object_versions().as_str());
            }

            if output.is_truncated() {
                println!("Next continuation token: {}", output.next_continuation_token());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: message: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
                _ => {
                    println!("Unknown error: {:?}", err);
                }
            }
        }
    }
}
```


<span id="470dfae7"></span>
### List all bucket inventory rules of a bucket

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
use ve_tos_rust_sdk::bucket::{ListBucketInventoryInput, ListBucketInventoryOutput};
use ve_tos_rust_sdk::error::TosError;
use ve_tos_rust_sdk::bucket::BucketInventoryConfiguration;

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
    let mut continuation_token = String::new();
    loop {
        let input = if continuation_token.is_empty() {
            ListBucketInventoryInput::new(bucket_name)
        } else {
            ListBucketInventoryInput::new_with_continuation_token(bucket_name, &continuation_token)
        };
        
        let output = client.list_bucket_inventory(&input).await;
        
        match output {
            Ok(output) => {
                println!("Is truncated: {}", output.is_truncated());
                println!("Number of configurations: {}", output.configurations().len());
                
                for (index, config) in output.configurations().iter().enumerate() {
                    println!("Configuration [{}]:", index);
                    println!("  id: {}", config.id());
                    println!("  is_enabled: {}", config.is_enabled());
                    if let Some(filter) = config.filter() {
                        println!("  filter prefix: {}", filter.prefix());
                    }
                    if let Some(dest) = config.destination() {
                        if let Some(tos_dest) = dest.tos_bucket_destination() {
                            println!("  destination bucket: {}", tos_dest.bucket());
                            println!("  destination prefix: {}", tos_dest.prefix());
                            println!("  destination format: {}", tos_dest.format().as_str());
                            println!("  destination role: {}", tos_dest.role());
                        }
                    }
                    if let Some(schedule) = config.schedule() {
                        println!("  schedule frequency: {}", schedule.frequency().as_str());
                    }
                    println!("  included object versions: {}", config.included_object_versions().as_str());
                    if let Some(opt_fields) = config.optional_fields() {
                        println!("  optional fields: {:?}", opt_fields.field());
                    }
                    println!("  is uncompressed: {}", config.is_un_compressed());
                }
                
                if output.is_truncated() {
                    continuation_token = output.next_continuation_token().to_string();
                } else {
                    break;
                }
            }
            Err(err) => {
                match err {
                    TosError::TosClientError { message, .. } => {
                        println!("Client error: message: {}", message);
                    }
                    TosError::TosServerError { request_id, ec, code, .. } => {
                        println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                    }
                    _ => {
                        println!("Unknown error: {:?}", err);
                    }
                }
                break;
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of ListBucketInventory, see [ListBucketInventory](https://docs.byteplus.com/docs/tos/ListBucketInventory).
