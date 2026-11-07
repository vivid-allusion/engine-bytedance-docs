---
title: "FetchObject（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/FetchObject"
---

The fetch_object interface fetches a single object up to 5 GiB in size from a public URL and writes it to the specified bucket. It supports encryption, ACL, and storage class settings. This article explains how to complete the fetch using the fetch_object interface in Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [regions and access domains](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Each call fetches only one object. The maximum object size is 5 GiB; fetching fails if exceeded.

* The `url` parameter only accepts publicly accessible addresses; private addresses will return an error.

* If `storage_class` is set, the destination object storage type follows this value; if not set, it inherits the bucket’s default type.

* When using SSE_C encryption, `ssec_algorithm`, `ssec_key`, and `ssec_key_md5` must all be provided.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, but IAM users have none by default. If a sub\-account needs to perform the fetch_object operation, the Volcengine main account must grant the following permissions to that sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5LuO5oyH5a6aLXVybC3mipPlj5blr7nosaE="></span>
### Fetch object from specified URL

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::object::{ObjectAPI};
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::error::TosError;
use ve_tos_rust_sdk::object::{FetchObjectInput};

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
    // Initialize logging
    let _guard = init_tracing_log("info", "temp/logs", "app.log");

    // Get credentials from environment variables
    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";

    // Build TOS client
    let client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build()
        .expect("Failed to build TOS client");

    // Prepare FetchObject input
    let mut input = FetchObjectInput::new("example-bucket", "target-object-key");
    input.set_url("https://example.com/public-source-file.txt"); // Required public URL
    input.set_ignore_same_key(true); // Optional: skip if target exists

    // Execute fetch object operation
    let result = client.fetch_object(&input).await;

    // Handle result
    match result {
        Ok(output) => {
            println!("Fetch successful!");
            println!("ETag: {}", output.etag());
            println!("Source Content Length: {}", output.source_content_length());
            println!("Source Content Type: {}", output.source_content_type());
            println!("MD5: {}", output.md5());
        },
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                },
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: Request ID: {}, EC: {}, Code: {}", request_id, ec, code);
                },
            }
        },
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the FetchObject API documentation, see [FetchObject](https://docs.byteplus.com/docs/tos/Fetchobject).
