---
title: "PutBucketPolicy（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketPolicy"
---

The put_bucket_policy interface modifies or creates a bucket policy, overwriting any existing one. This article explains how to set a bucket policy using the put_bucket_policy interface of the Rust SDK. It requires the bucket owner or an authorized sub\-account to call it, and the total policy size must not exceed 20 KB.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The total size of the bucket policy JSON after serialization must not exceed 20 KB.

* The new policy completely overwrites the existing one, replacing all previous content.

* There is no limit on the number of policy statements, but the JSON format must be valid and comply with syntax rules.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the put_bucket_policy operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [Bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutBucketPolicy

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".6K6-572u5a2Y5YKo5qG2562W55Wl"></span>
### Set bucket policy

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
use ve_tos_rust_sdk::bucket::PutBucketPolicyInput;
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

    let ak = env::var("TOS_ACCESS_KEY").unwrap_or(""
        .to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or(""
        .to_string());
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

    // Create bucket policy input
    let bucket_name = "my-bucket";
    let policy = r#"{
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "Bucket read-only policy",
                "Effect": "Allow",
                "Principal": ["210004xxxx"],
                "Action": ["tos:Get*", "tos:List*"],
                "Resource": ["trn:tos:::my-bucket", "trn:tos:::my-bucket/*"]
            }
        ]
    }"#;
    let mut input = PutBucketPolicyInput::new(bucket_name);
    input.set_policy(policy);

    // Call the bucket policy setting interface
    let output = client.put_bucket_policy(&input).await;
    match output {
        Ok(output) => {
            let request_id = output.request_id();
            println!("Bucket policy configured successfully，Request ID: {}", request_id);
            // Check request ID length
            assert!(request_id.len() > 0, "Request ID cannot be empty");
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, .. } => {
                    println!("Server error - Request ID: {}, Error code: {}", request_id, ec);
                }
            }
        }
    }
}

```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on PutBucketPolicy, refer to [PutBucketPolicy](https://docs.byteplus.com/docs/tos/reference-putbucketpolicy).
