---
title: "AppendObject（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/AppendObject"
---

The append_object interface is used for appending data to an object. This article explains how to use the Rust SDK's append_object interface to append data at a specified offset, supporting concurrent and safe writing to Appendable objects up to 5 GB.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [region and access domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, this example code requires reading the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, you need to configure long\-term access credentials. For details, see [configure long-term access credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* The size of the object after appending must not exceed 5 GB; exceeding this limit causes append_object to fail.

* Setting `content_type` is only allowed when `offset` is `0`. This parameter will be ignored in subsequent appends.

* append_object does not support server\-side encryption. Setting related encryption headers will return an error.

* Concurrent append_object calls on the same appendable_object may cause conflicts. Serial calls are recommended.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The Volcengine main account has all permissions by default, but IAM users have no permissions by default. If you need to perform the append_object operation using a sub\-account, the Volcengine main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutObject

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id="407da04d"></span>
### Append upload string

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
use ve_tos_rust_sdk::object::{AppendObjectInput};
use ve_tos_rust_sdk::asynchronous::tos::{new_stream, BufferStream};
use ve_tos_rust_sdk::error::TosError;
use std::io::Cursor;

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
    let object_name = "example-object";
    let data = "your append object value";
    let stream = new_stream(data);
    let mut input = AppendObjectInput::<BufferStream>::new_with_content(bucket_name, object_name, stream);
    let output = client.append_object(&input).await;

    match output {
        Ok(output) => {
            println!("Request ID: {}", output.request_id());
            println!("Next Append Offset{}", output.next_append_offset())
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => println!("Client Error: {}", message),
                TosError::TosServerError { request_id, ec, code, .. } => println!("Server Error: RequestID={}, Code={}, Message={}", request_id, code, ec),
                _ => println!("Unexpected Error: {:?}", err)
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation of AppendObject, see [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject).
