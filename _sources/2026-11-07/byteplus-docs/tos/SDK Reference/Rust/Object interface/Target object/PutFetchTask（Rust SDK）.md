---
title: "PutFetchTask（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutFetchTask"
---

The put_fetch_task interface creates asynchronous fetch tasks, fetching single files from public URLs and writing them into specified TOS buckets. This article explains how to submit tasks via the Rust SDK's put_fetch_task interface and obtain a TaskID for subsequent result queries.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term credentials. For details, see [configure long-term credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* A single fetch supports only one object, with a maximum object size of 500 GiB. The put_fetch_task will fail if exceeded.

* The `url` parameter must point to a publicly accessible resource; otherwise, put_fetch_task cannot complete the fetch.

* If `content_md5` is set, TOS will verify the fetched content’s MD5. If it does not match, put_fetch_task will return a failure.

* Layered bucket types do not currently support put_fetch_task. Please confirm the bucket type before calling.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the put_fetch_task operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutFetchTask

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Yib5bu65LuO5oyH5a6aLXVybC3mipPlj5botYTmupDnmoTlvILmraXku7vliqE="></span>
### Create an asynchronous task to fetch resources from the specified URL

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
use ve_tos_rust_sdk::object::PutFetchTaskInput;
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

    // Create an asynchronous task to fetch resources from a specified URL
    let input = PutFetchTaskInput::new_with_url("example-bucket", "target-object-key", "https://example.com/source-file.txt");
    let output = client.put_fetch_task(&input).await;
    match output {
        Ok(output) => {
            println!("task_id: {}", output.task_id());
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("message: {}", message);
                }
                TosError::TosServerError { request_id, ec, code ,.. } =>  {
                    println!("Server error: request_id: {}, ec: {}, code: {}", request_id, ec, code);
                }
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on PutFetchTask, see [PutFetchTask](https://docs.byteplus.com/docs/tos/Putfetchtask).
