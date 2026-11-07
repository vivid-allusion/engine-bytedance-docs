---
title: "PutBucketReplication（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketReplication"
---

The put_bucket_replication interface sets cross\-region or same\-region replication rules for buckets. This article explains how to configure object replication using the put_bucket_replication interface in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, this example code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you must configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Tiered buckets do not support the put_bucket_replication call.

* Before cross\-account replication, you must first grant read permissions to the source bucket and write permissions to the target bucket.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have none by default. If you need to use a sub\-account to perform the put_bucket_replication operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutBucketReplication

<span id=".5Luj56CB56S65L6L"></span>
## Code examples

<span id=".5Yib5bu65aSN5Yi26KeE5YiZ5pe25oyH5a6a5aSa5Liq5YmN57yA"></span>
### Specify multiple prefixes when creating replication rules

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
use ve_tos_rust_sdk::bucket::{PutBucketReplicationInput, ReplicationRule, Destination };
use ve_tos_rust_sdk::enumeration::{StatusType};

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

    // Specify copy rules for multiple prefixes
    let mut input = PutBucketReplicationInput::new("source-bucket", "ServiceRoleforReplicationAccessTOS");
    let mut rule = ReplicationRule::new("multi-prefix-rule");
    rule.set_status(StatusType::StatusEnabled);
    rule.set_historical_object_replication(StatusType::StatusEnabled);
    rule.set_prefix_set(vec!["prefix1/".to_string(), "prefix2/".to_string()]);
    let dest = Destination::new("target-bucket", "cn-beijing");
    rule.set_destination(dest);
    input.add_rule(rule);

    let result = client.put_bucket_replication(&input).await;
    match result {
        Ok(_) => println!("Copy rules with multiple prefixes set successfully"),
        Err(e) => eprintln!("Failed to set copy rules with multiple prefixes: {:?}", e)
    }
}

```


<span id=".6K6-572u5aSN5Yi26KeE5YiZ55qE5a2Y5YKo57G75Z6L5ZKM57un5om_562W55Wl"></span>
### Set storage type and inheritance policy for replication rules

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
use ve_tos_rust_sdk::bucket::{PutBucketReplicationInput, ReplicationRule, Destination };
use ve_tos_rust_sdk::enumeration::{StatusType, StorageClassType, StorageClassInheritDirectiveType};

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

    // Configure replication rules for storage type and inheritance policy.
    let mut input = PutBucketReplicationInput::new("source-bucket", "ServiceRoleforReplicationAccessTOS");
    let mut rule = ReplicationRule::new("storage-class-rule");
    rule.set_status(StatusType::StatusEnabled);
    rule.set_historical_object_replication(StatusType::StatusEnabled);
    let mut dest = Destination::new("target-bucket", "cn-beijing");
    dest.set_storage_class(StorageClassType::StorageClassIa);
    dest.set_storage_class_inherit_directive(StorageClassInheritDirectiveType::StorageClassIDSourceObject);
    rule.set_destination(dest);
    input.add_rule(rule);

    let result = client.put_bucket_replication(&input).await;
    match result {
        Ok(_) => println!("Replication rules with storage type and inheritance strategy set up successfully."),
        Err(e) => eprintln!("Replication rule setup with storage type and inheritance strategy failed: {:?}", e)
    }
}

```


<span id=".6K6-572u5a2Y5YKo5qG255qE6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
### Set cross\-region replication rules for buckets

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
use ve_tos_rust_sdk::bucket::{PutBucketReplicationInput, ReplicationRule, Destination};
use ve_tos_rust_sdk::enumeration::StatusType;

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

    // Configure cross-region copying rules
    let mut input = PutBucketReplicationInput::new("source-bucket", "ServiceRoleforReplicationAccessTOS");
    let mut rule = ReplicationRule::new("cross-region-rule");
    rule.set_status(StatusType::StatusEnabled);
    rule.set_historical_object_replication(StatusType::StatusEnabled);
    let dest = Destination::new("target-bucket", "cn-shanghai");
    rule.set_destination(dest);
    input.add_rule(rule);

    let result = client.put_bucket_replication(&input).await;
    match result {
        Ok(_) => println!("Cross-region copying rules set successfully"),
        Err(e) => eprintln!("Cross-region copy rule settings failed: {:?}", e)
    }
}

```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on PutBucketReplication, see [PutBucketReplication](https://docs.byteplus.com/docs/tos/Putbucketreplication).
