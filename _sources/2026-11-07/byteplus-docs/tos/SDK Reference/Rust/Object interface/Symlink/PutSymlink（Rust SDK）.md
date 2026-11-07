---
title: "PutSymlink（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutSymlink"
---

The put_symlink interface creates a symlink for an existing TOS object. The Rust SDK uses this interface to generate a shortcut path pointing to the target file.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to specify the region and the access domain name in the sample code according to your situation. For details, see [region and access domain name](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, this sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* When calling put_symlink, `symlink_target_key` must be provided and cannot point to another symlink.

* The symlink and the target object must be in the same region. `symlink_target_bucket` supports only different buckets within the same region.

* If versioning is enabled for the bucket, the `forbid_overwrite` setting no longer applies, and the object with the same name will still be overwritten.

* Secondary symlinks cannot be accessed via get_object. put_symlink supports only first\-level symlinks.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to perform the put_symlink operation using a sub\-account, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yib5bu66L2v6L-e5o6l"></span>
### Creating symlinks

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::object::ObjectAPI;
use ve_tos_rust_sdk::common::init_tracing_log;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::object::{PutObjectInput, PutSymlinkInput};
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

    // Create target object first
    let target_bucket = "example-bucket";
    let target_key = "example-object";

    // Create normal soft link
    let symlink_key = "symlink-normal.txt";
    let symlink_input = PutSymlinkInput::new(target_bucket, target_key, symlink_key);

    let symlink_output = client.put_symlink(&symlink_input).await;
    match symlink_output {
        Ok(output) => {
            println!("Normal soft link created successfully. Version ID: {}", output.version_id());
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

For API documentation on PutSymlink, refer to [PutSymlink](https://docs.byteplus.com/docs/tos/Putsymlink).
