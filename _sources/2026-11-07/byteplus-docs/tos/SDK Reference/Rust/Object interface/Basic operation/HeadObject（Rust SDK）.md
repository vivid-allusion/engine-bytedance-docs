---
title: "HeadObject（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/HeadObject"
---

The head_object interface retrieves object metadata without returning the object itself. This article explains how to use the head_object interface in the Rust SDK to perform this operation and handle encryption scenarios such as SSE\-C.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual conditions. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Before using the SDK, you need to configure long\-term credentials. For details, see [configure long-term credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* If the object is encrypted with SSE\-TOS or SSE\-KMS, the head_object request must not include `x_tos_server_side_encryption` headers; otherwise, it returns 400 BadRequest.

* If the object is encrypted with SSE\-C, the head_object request must include `x_tos_server_side_encryption_customer_algorithm`, `x_tos_server_side_encryption_customer_key`, and `x_tos_server_side_encryption_customer_key_md5`. All three are mandatory.

* For symlink objects, `ETag`, `x_tos_storage_class`, `x_tos_hash_crc64ecma`, and `x_tos_symlink_target_size` return the target object's values; `Last-Modified` is the later of the symlink and target object; other headers return the symlink object's values.

* When the request header includes the `version_id` parameter, head_object returns metadata for the specified version of the object; if the version does not exist, it responds with 404 Not Found.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, but an IAM user has no permissions by default. If you need a sub\-account to perform the head_object operation, the Volcengine main account must grant the following permissions to the sub\-account through the [IAM policy](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policy](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5p-l6K-i5a-56LGh5YWD5pWw5o2u5L-h5oGv"></span>
### Query object metadata information

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
use ve_tos_rust_sdk::object::HeadObjectInput;
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

    let input = HeadObjectInput::new("example-bucket", "example-object.txt");
    let output = client.head_object(&input).await;
    match output {
        Ok(output) => {
            println!("etag: {}", output.etag());
            if let Some(last_modified) = output.last_modified() {
                println!("last_modified: {}", last_modified);
            }
            println!("delete_marker: {}", output.delete_marker());
            println!("version_id: {}", output.version_id());
            println!("object_type: {}", output.object_type());
            println!("hash_crc64ecma: {}", output.hash_crc64ecma());
            if let Some(storage_class) = output.storage_class() {
                println!("storage_class: {:?}", storage_class);
            }
            println!("meta entries:");
            for (key, value) in output.meta() {
                println!("  {}: {}", key, value);
            }
            println!("content_length: {}", output.content_length());
            println!("cache_control: {}", output.cache_control());
            println!("content_disposition: {}", output.content_disposition());
            println!("content_encoding: {}", output.content_encoding());
            println!("content_language: {}", output.content_language());
            println!("content_type: {}", output.content_type());
            if let Some(expires) = output.expires() {
                println!("expires: {}", expires);
            }
            println!("is_directory: {}", output.is_directory());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error message: {}", message);
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

For the HeadObject API documentation, see [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject).
