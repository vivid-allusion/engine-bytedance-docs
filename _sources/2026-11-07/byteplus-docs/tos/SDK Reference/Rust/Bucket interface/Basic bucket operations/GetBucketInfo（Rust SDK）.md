---
title: "GetBucketInfo（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketInfo"
---

The get_bucket_info interface queries bucket configuration information. This article explains how to use the get_bucket_info interface in the Rust SDK to obtain full metadata such as name, region, storage type, and encryption rules.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain name in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the get_bucket_info operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetBucketInfo

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="8c4272ab"></span>
### Retrieve details of the specified bucket

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
use ve_tos_rust_sdk::bucket::GetBucketInfoInput;
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
    let input = GetBucketInfoInput::new(bucket_name);
    let output = client.get_bucket_info(&input).await;
    match output {
        Ok(output) => {
            let bucket_info = output.bucket();
            println!("Bucket info:");
            println!("name: {}", bucket_info.name());
            println!("owner:");
            println!("  id: {}", bucket_info.owner().id());
            if let Some(date) = bucket_info.creation_date() {
                println!("creation_date: {}", date);
            }
            if let Some(sc) = bucket_info.storage_class() {
                println!("storage_class: {}", sc.as_str());
            }
            println!("project_name: {}", bucket_info.project_name());
            if let Some(bt) = bucket_info.bucket_type() {
                println!("bucket_type: {}", bt.as_str());
            }
            println!("location: {}", bucket_info.location());
            if let Some(az) = bucket_info.az_redundancy() {
                println!("az_redundancy: {}", az.as_str());
            }
            println!("extranet_endpoint: {}", bucket_info.extranet_endpoint());
            println!("intranet_endpoint: {}", bucket_info.intranet_endpoint());
            println!("extranet_s3_endpoint: {}", bucket_info.extranet_s3_endpoint());
            println!("intranet_s3_endpoint: {}", bucket_info.intranet_s3_endpoint());
            if let Some(vs) = bucket_info.versioning() {
                println!("versioning: {}", vs.as_str());
            }
            if let Some(crr) = bucket_info.cross_region_replication() {
                println!("cross_region_replication: {}", crr.as_str());
            }
            if let Some(ta) = bucket_info.transfer_acceleration() {
                println!("transfer_acceleration: {}", ta.as_str());
            }
            if let Some(am) = bucket_info.access_monitor() {
                println!("access_monitor: {}", am.as_str());
            }
            let sse_config = bucket_info.server_side_encryption_configuration();
            println!("server_side_encryption_configuration:");
            let rule = &sse_config.rule();
            println!("  rule:");
            let apply_default = &rule.apply_server_side_encryption_by_default();
            println!("    apply_server_side_encryption_by_default:");
            println!("      sse_algorithm: {}", apply_default.sse_algorithm());
            println!("      kms_master_key_id: {}", apply_default.kms_master_key_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: message: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
                _ => println!("Unexpected error: {:?}", err),
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of GetBucketInfo, see [GetBucketInfo](https://docs.byteplus.com/docs/tos/Getbucketinfo).
