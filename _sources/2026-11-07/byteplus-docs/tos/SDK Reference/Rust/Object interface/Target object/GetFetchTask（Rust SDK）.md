---
title: "GetFetchTask（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetFetchTask"
---

The get_fetch_task API queries the details of an asynchronous fetch task, including status and callback information. The Rust SDK example shows how to pass taskId to obtain results, supporting only tasks within 72 hours.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Region and Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, configure long\-term credentials. For details, see [Configuring Long-term Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* get_fetch_task only supports querying tasks within 72 hours; results cannot be returned after expiration.

* Layered buckets do not support get_fetch_task. Confirm the bucket type before calling.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need a sub\-account to perform the get_fetch_task operation, the BytePlus main account must grant the sub\-account the following permissions through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:GetFetchTask

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5p-l6K-i5oqT5Y-W5Lu75Yqh55qE6K-m57uG5L-h5oGv"></span>
### Query detailed information of fetch tasks

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
use ve_tos_rust_sdk::object::{GetFetchTaskInput};
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

    // Prepare input for GetFetchTask
    let bucket = "example-bucket";
    let task_id = "3b35b85c-b724-***";
    let input = GetFetchTaskInput::new(bucket, task_id);

    // Call GetFetchTask API
    let result = client.get_fetch_task(&input).await;
    match result {
        Ok(output) => {
            println!("state: {}", output.state());
            if !output.err().is_empty() {
                println!("err: {}", output.err());
            }
            if let Some(task) = output.task() {
                println!("task.url: {}", task.url());
                println!("task.ignore_same_key: {}", task.ignore_same_key());
                println!("task.content_md5: {}", task.content_md5());
                println!("task.bucket: {}", task.bucket());
                println!("task.key: {}", task.key());
                println!("task.callback_url: {}", task.callback_url());
                println!("task.callback_host: {}", task.callback_host());
                println!("task.callback_body_type: {}", task.callback_body_type());
                println!("task.callback_body: {}", task.callback_body());
                if let Some(sc) = task.storage_class() {
                    println!("task.storage_class: {}", sc.as_str());
                }
                if let Some(acl) = task.acl() {
                    println!("task.acl: {}", acl.as_str());
                }
                println!("task.grant_fullcontrol: {}", task.grant_fullcontrol());
                println!("task.grant_read: {}", task.grant_read());
                println!("task.grant_read_acp: {}", task.grant_read_acp());
                println!("task.grant_write: {}", task.grant_write());
                println!("task.grant_write_acp: {}", task.grant_write_acp());
                println!("task.ssec_algorithm: {}", task.ssec_algorithm());
                println!("task.ssec_key: {}", task.ssec_key());
                println!("task.ssec_key_md5: {}", task.ssec_key_md5());
                println!("task.user_meta entries:");
                for (idx, meta) in task.meta().iter().enumerate() {
                    println!("  [{}] key: {}, value: {}", idx, meta.0, meta.1);
                }
                println!("task.meta entries:");
                for (k, v) in task.meta().iter() {
                    println!("  {}: {}", k, v);
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

For the API documentation of GetFetchTask, see [GetFetchTask](https://docs.byteplus.com/docs/tos/Getfetchtask).
