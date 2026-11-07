---
title: "PreSignedURL（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PreSignedURL"
---

The pre_signed_url interface generates signed temporary upload or download URLs. This article explains how to obtain and directly access the object URL using the pre_signed_url interface in the Rust SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You must fill in the region and endpoint in the sample code according to your actual situation. For details, see [Regions and endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, this example reads the Access Key ID and Secret Access Key from environment variables. Before using the SDK, configure long\-term access credentials. For details, see [Configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The pre_signed_url validity period is controlled by the expires parameter in seconds, with a maximum of 7 days.

* When uploading with pre_signed_url, the http_method must match the method specified during generation; otherwise, a 403 error is returned.


&nbsp;

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIrkvKDlr7nosaE="></span>
### Upload objects using a pre\-signed URL

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::enumeration::{HttpMethodType};
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::auth::{PreSignedURLInput, SignerAPI};
use reqwest::Client as HttpClient;
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

    // 1. Upload object using pre-signed URL
    let bucket = "example-bucket";
    let key = "test-upload-object.txt";
    let mut upload_input = PreSignedURLInput::new_with_key(bucket, key);
    upload_input.set_http_method(HttpMethodType::HttpMethodPut);
    upload_input.set_expires(3600); // validity period 1 hour

    let upload_output = client.pre_signed_url(&upload_input);
    match upload_output {
        Ok(output) => {
            println!("Pre-signed URL for upload: {}", output.signed_url());
            // Upload object using reqwest client
            let http_client = HttpClient::new();
            let upload_response = http_client.put(output.signed_url())
                .body("Hello from pre-signed URL upload")
                .send()
                .await;
            match upload_response {
                Ok(resp) if resp.status().is_success() => {
                    println!("Upload successful with status: {}", resp.status());
                }
                Ok(resp) => {
                    println!("Upload failed with status: {}", resp.status());
                }
                Err(e) => {
                    println!("Upload request error: {}", e);
                }
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIvovb3lr7nosaE="></span>
### Download objects using pre\-signed URL

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::enumeration::{HttpMethodType};
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::auth::{PreSignedURLInput, SignerAPI};
use reqwest::Client as HttpClient;
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

    // 2. Download objects using pre-signed URL
    let bucket = "example-bucket";
    let key = "test-download-object.txt";
    let mut download_input = PreSignedURLInput::new_with_key(bucket, key);
    download_input.set_http_method(HttpMethodType::HttpMethodGet);
    download_input.set_expires(3600);

    let download_output = client.pre_signed_url(&download_input);
    match download_output {
        Ok(output) => {
            println!("Pre-signed URL for download: {}", output.signed_url());
            // Download objects using reqwest client
            let http_client = HttpClient::new();
            let download_response = http_client.get(output.signed_url())
                .send()
                .await;
            match download_response {
                Ok(resp) if resp.status().is_success() => {
                    let content = resp.text().await.unwrap();
                    println!("Download successful, content: {}", content);
                }
                Ok(resp) => {
                    println!("Download failed with status: {}", resp.status());
                }
                Err(e) => {
                    println!("Download request error: {}", e);
                }
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3liKDpmaTlr7nosaE="></span>
### Delete objects using pre\-signed URL

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::enumeration::{HttpMethodType};
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::auth::{PreSignedURLInput, SignerAPI};
use reqwest::Client as HttpClient;
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

    // 3. Delete object using pre-signed URL
    let bucket = "example-bucket";
    let key = "test-delete-object.txt";
    let mut delete_input = PreSignedURLInput::new_with_key(bucket, key);
    delete_input.set_http_method(HttpMethodType::HttpMethodDelete);
    delete_input.set_expires(3600);

    let delete_output = client.pre_signed_url(&delete_input);
    match delete_output {
        Ok(output) => {
            println!("Pre-signed URL for delete: {}", output.signed_url());
            // Delete object using reqwest client
            let http_client = HttpClient::new();
            let delete_response = http_client.delete(output.signed_url())
                .send()
                .await;
            match delete_response {
                Ok(resp) if resp.status().is_success() => {
                    println!("Delete successful with status: {}", resp.status());
                }
                Ok(resp) => {
                    println!("Delete failed with status: {}", resp.status());
                }
                Err(e) => {
                    println!("Delete request error: {}", e);
                }
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("Client error: {}", message);
                }
                TosError::TosServerError { request_id, ec, code, .. } => {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on PreSignedURL, see [URL containing signature](https://docs.byteplus.com/docs/tos/reference-including-a-signature-in-the-url).
