---
title: "CreateBucket (Rust SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/CreateBucket"
---

The create_bucket API creates a TOS bucket and sets its default storage class. This article explains how to create a bucket and configure permissions through the Rust SDK's create_bucket API.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and endpoint in the sample code according to your situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term credentials. For details, see [Configure long-term credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Each account can create up to 100 buckets across all regions. Calls exceeding this limit will return an error.

* To use the DEEP_COLD_ARCHIVE storage class, it is only supported in China (Beijing), China (Shanghai), and China (Guangzhou). It is currently in closed beta; please contact your account manager to enable it.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The main account has all permissions by default, but IAM users have none by default. If you need a sub\-account to perform the create_bucket operation, the main account must grant the sub\-account the following permissions through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:CreateBucket

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="6af912e5"></span>
### Create a bucket with standard storage type

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
use ve_tos_rust_sdk::bucket::CreateBucketInput;

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
    init_tracing_log("info", "temp/logs", "app.log");

    let ak = env::var("TOS_ACCESS_KEY").unwrap_or_default();
    let sk = env::var("TOS_SECRET_KEY").unwrap_or_default();
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";

    let client = tos::builder::<TokioRuntime>()
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    let bucket_name = "my-standard-bucket";
    let input = CreateBucketInput::new(bucket_name);

    match client.create_bucket(&input).await {
        Ok(output) => println!("Bucket created successfully. Location: {}", output.location()),
        Err(e) => eprintln!("Error creating bucket: {:?}", e),
    }
}
```


<span id="c4c0f860"></span>
### Create a bucket with a specific storage type and permissions

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
use ve_tos_rust_sdk::bucket::CreateBucketInput;
use ve_tos_rust_sdk::enumeration::{ACLType, StorageClassType};

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
    init_tracing_log("info", "temp/logs", "app.log");

    let ak = env::var("TOS_ACCESS_KEY").unwrap_or_default();
    let sk = env::var("TOS_SECRET_KEY").unwrap_or_default();
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";

    let client = tos::builder::<TokioRuntime>()
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    let bucket_name = "my-ia-public-bucket";
    let mut input = CreateBucketInput::new(bucket_name);
    input.set_storage_class(StorageClassType::StorageClassIa);
    input.set_acl(ACLType::ACLPublicRead);

    match client.create_bucket(&input).await {
        Ok(output) => println!("Bucket created successfully. Location: {}", output.location()),
        Err(e) => eprintln!("Error creating bucket: {:?}", e),
    }
}
```


<span id="3c787c03"></span>
### Create a multi\-availability zone redundant bucket

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
use ve_tos_rust_sdk::bucket::CreateBucketInput;
use ve_tos_rust_sdk::enumeration::AzRedundancyType;

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
    init_tracing_log("info", "temp/logs", "app.log").unwrap();

    let ak = env::var("TOS_ACCESS_KEY").unwrap_or_default();
    let sk = env::var("TOS_SECRET_KEY").unwrap_or_default();
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";

    let client = tos::builder::<TokioRuntime>()
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build().unwrap();

    let bucket_name = "my-multi-az-bucket";
    let mut input = CreateBucketInput::new(bucket_name);
    input.set_az_redundancy(AzRedundancyType::AzRedundancyMultiAz);

    match client.create_bucket(&input).await {
        Ok(output) => println!("Bucket created successfully. Location: {}", output.location()),
        Err(e) => eprintln!("Error creating bucket: {:?}", e),
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of CreateBucket, see [CreateBucket](https://docs.byteplus.com/docs/tos/reference-createbucket).
