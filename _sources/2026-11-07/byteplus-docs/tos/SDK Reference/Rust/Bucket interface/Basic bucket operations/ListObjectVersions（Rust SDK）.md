---
title: "ListObjectVersions（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/ListObjectVersions"
---

The list_object_versions interface lists multiple versions of objects in a bucket, supporting pagination and prefix filtering. This article explains how to obtain a list of multiple versions using the list_object_versions interface of the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, this sample code reads the Access Key ID and Secret Access Key from environment variables. Before using the SDK, you must configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Hierarchical buckets do not support the ListObjectVersions interface.

* Each request returns up to 1,000 multi\-version objects.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. To allow a sub\-account to perform the list_object_versions operation, the BytePlus main account must grant the following permissions to that sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:ListObjectVersions

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="3bbf8c49"></span>
### Simple listing

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
use ve_tos_rust_sdk::object::ListObjectVersionsInput;
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

    // List all object versions of specified bucket
    let mut input = ListObjectVersionsInput::new("example-bucket-2");
    input.set_max_keys(100);
    let output = client.list_object_versions(&input).await;

    match output {
        Ok(output) => {
            println!("name: {}", output.name());
            println!("prefix: {}", output.prefix());
            println!("key_marker: {}", output.key_marker());
            println!("version_id_marker: {}", output.version_id_marker());
            println!("max_keys: {}", output.max_keys());
            println!("delimiter: {}", output.delimiter());
            println!("is_truncated: {}", output.is_truncated());
            println!("encoding_type: {}", output.encoding_type());
            println!("next_key_marker: {}", output.next_key_marker());
            println!("next_version_id_marker: {}", output.next_version_id_marker());

            println!("common_prefixes:");
            for (idx, prefix) in output.common_prefixes().iter().enumerate() {
                println!("[{}]: prefix: {}, last_modified: {:?}",
                         idx,
                         prefix.prefix(),
                         prefix.last_modified().map(|dt| dt.format("%Y-%m-%dT%H:%M:%SZ").to_string())
                );
            }

            println!("versions:");
            for (idx, version) in output.versions().iter().enumerate() {
                println!("[{}]:", idx);
                println!("  key: {}", version.key());
                println!("  last_modified: {:?}", version.last_modified().map(|dt| dt.format("%Y-%m-%dT%H:%M:%SZ").to_string()));
                println!("  etag: {}", version.etag());
                println!("  is_latest: {}", version.is_latest());
                println!("  size: {}", version.size());
                println!("  owner:");
                println!("    id: {}", version.owner().id());
                println!("  storage_class: {:?}", version.storage_class());
                println!("  version_id: {}", version.version_id());
                println!("  hash_crc64ecma: {}", version.hash_crc64ecma());
            }

            println!("delete_markers:");
            for (idx, marker) in output.delete_markers().iter().enumerate() {
                println!("[{}]:", idx);
                println!("  key: {}", marker.key());
                println!("  last_modified: {:?}", marker.last_modified().map(|dt| dt.format("%Y-%m-%dT%H:%M:%SZ").to_string()));
                println!("  is_latest: {}", marker.is_latest());
                println!("  owner:");
                println!("    id: {}", marker.owner().id());
                println!("  version_id: {}", marker.version_id());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: message: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, status_code: {}, code: {}", request_id, ec, code);
                }
                _ => println!("Unknown error: {:?}", err),
            }
        }
    }
}
```


<span id="3f1724d7"></span>
### List object versions with a specified prefix

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
use ve_tos_rust_sdk::object::ListObjectVersionsInput;
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

    // List object versions with specified prefix
    let mut input = ListObjectVersionsInput::new("example-bucket-2");
    input.set_prefix("docs/");
    input.set_max_keys(100);
    let output = client.list_object_versions(&input).await;

    match output {
        Ok(output) => {
            println!("name: {}", output.name());
            println!("prefix: {}", output.prefix());
            println!("key_marker: {}", output.key_marker());
            println!("version_id_marker: {}", output.version_id_marker());
            println!("max_keys: {}", output.max_keys());
            println!("delimiter: {}", output.delimiter());
            println!("is_truncated: {}", output.is_truncated());
            println!("encoding_type: {}", output.encoding_type());
            println!("next_key_marker: {}", output.next_key_marker());
            println!("next_version_id_marker: {}", output.next_version_id_marker());

            println!("common_prefixes:");
            for (idx, prefix) in output.common_prefixes().iter().enumerate() {
                println!("[{}]: prefix: {}, last_modified: {:?}",
                         idx,
                         prefix.prefix(),
                         prefix.last_modified().map(|dt| dt.format("%Y-%m-%dT%H:%M:%SZ").to_string())
                );
            }

            println!("versions:");
            for (idx, version) in output.versions().iter().enumerate() {
                println!("[{}]:", idx);
                println!("  key: {}", version.key());
                println!("  last_modified: {:?}", version.last_modified().map(|dt| dt.format("%Y-%m-%dT%H:%M:%SZ").to_string()));
                println!("  etag: {}", version.etag());
                println!("  is_latest: {}", version.is_latest());
                println!("  size: {}", version.size());
                println!("  owner:");
                println!("    id: {}", version.owner().id());
                println!("  storage_class: {:?}", version.storage_class());
                println!("  version_id: {}", version.version_id());
                println!("  hash_crc64ecma: {}", version.hash_crc64ecma());
            }

            println!("delete_markers:");
            for (idx, marker) in output.delete_markers().iter().enumerate() {
                println!("[{}]:", idx);
                println!("  key: {}", marker.key());
                println!("  last_modified: {:?}", marker.last_modified().map(|dt| dt.format("%Y-%m-%dT%H:%M:%SZ").to_string()));
                println!("  is_latest: {}", marker.is_latest());
                println!("  owner:");
                println!("    id: {}", marker.owner().id());
                println!("  version_id: {}", marker.version_id());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: message: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, status_code: {}, code: {}", request_id, ec, code);
                }
                _ => println!("Unknown error: {:?}", err),
            }
        }
    }
}
```


&nbsp;

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For API documentation about ListObjectVersions, see [ListObjectVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions).
