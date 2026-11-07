---
title: "GetBucketReplication（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketReplication"
---

The get_bucket_replication interface retrieves the cross\-region or same\-region replication rules and progress of a specified bucket. This article explains how to query replication configurations and status using the get_bucket_replication interface in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code in this article reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Tiered buckets do not support calling the get_bucket_replication interface.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users do not have any permissions by default. If you need to perform get_bucket_replication operations using a sub\-account, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketReplication

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5oyH5a6a6KeE5YiZLWlkLeiOt-WPluWtmOWCqOahtuWkjeWItumFjee9rg=="></span>
### Get bucket replication configuration by rule ID

```Rust
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::GetBucketReplicationInput;
use ve_tos_rust_sdk::error::TosError;

#[derive(Debug, Default)]
pub struct TokioRuntime {}

#[async_trait::async_trait]
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
    let ak = env::var("TOS_ACCESS_KEY").expect("TOS_ACCESS_KEY is not set");
    let sk = env::var("TOS_SECRET_KEY").expect("TOS_SECRET_KEY is not set");
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    
    // Building an asynchronous TOS client
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().expect("Client build failed");
    
    // Bucket name and rule ID
    let bucket_name = "your-bucket-name";
    let rule_id = "rule-123";
    
    // Build a bucket replication configuration input to obtain a specified rule ID.
    let mut input = GetBucketReplicationInput::default();
    input.set_bucket(bucket_name);
    input.set_rule_id(rule_id);
    
    // Calling the API
    let result = client.get_bucket_replication(&input).await;
    
    match result {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            println!("Copy character: {}", output.role());
            
            // Rules for finding a specified ID
            if let Some(rule) = output.rules().iter().find(|r| r.id() == rule_id) {
                println!("\nFind the rules ID={}:", rule_id);
                println!("  Status: {:?}", rule.status());
                println!("  Prefix set: {:?}", rule.prefix_set());
                println!("  Target bucket: {}", rule.destination().bucket());
                println!("  Historical object copy status: {:?}", rule.historical_object_replication());
            } else {
                println!("No rule found ID={}", rule_id);
            }
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    eprintln!("Client error: {}", message);
                },
                TosError::TosServerError { request_id, ec, .. } => {
                    eprintln!("Server error: Request ID={}, Error code={}", request_id, ec);
                },
                _ => {
                    eprintln!("Unknown error: {:?}", err);
                }
            }
        }
    }
}

```


<span id=".6I635Y-W5a2Y5YKo5qG25aSN5Yi26YWN572u"></span>
### Get bucket replication configuration

```Rust
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::GetBucketReplicationInput;
use ve_tos_rust_sdk::error::TosError;

#[derive(Debug, Default)]
pub struct TokioRuntime {}

#[async_trait::async_trait]
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
    let ak = env::var("TOS_ACCESS_KEY").expect("TOS_ACCESS_KEY未设置");
    let sk = env::var("TOS_SECRET_KEY").expect("TOS_SECRET_KEY未设置");
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    
    // Building an asynchronous TOS client
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().expect("Client build failed");
    
    // Bucket name
    let bucket_name = "your-bucket-name";
    
    // Build input to obtain bucket replication configuration
    let mut input = GetBucketReplicationInput::default();
    input.set_bucket(bucket_name);
    
    // Call the API to get bucket replication configuration
    let result = client.get_bucket_replication(&input).await;
    
    match result {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            println!("Copy role: {}", output.role());
            println!("Number of copy rules: {}", output.rules().len());
            
            for (index, rule) in output.rules().iter().enumerate() {
                println!("\nrules {}:", index + 1);
                println!("  ID: {}", rule.id());
                println!("  Status: {:?}", rule.status());
                println!("  Prefix set: {:?}", rule.prefix_set());
                println!("  Target storage bucket: {}", rule.destination().bucket());
                println!("  Target region: {}", rule.destination().location());
            }
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    eprintln!("Client error: {}", message);
                },
                TosError::TosServerError { request_id, ec, .. } => {
                    eprintln!("Server error: Request ID={}, Error code={}", request_id, ec);
                },
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

For API documentation about GetBucketReplication, see [GetBucketReplication](https://docs.byteplus.com/docs/tos/Getbucketreplication).
