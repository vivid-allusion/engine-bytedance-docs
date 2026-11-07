---
title: "Initialize the client (Rust SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Initialize_the_client_Rust_SDK"
---

This article introduces example code for initializing the client and common configuration scenarios.

<span id="73cbef87"></span>
## Prerequisites

[Rust SDK installed](https://docs.byteplus.com/docs/tos/Install_Rust_SDK).

<span id="b0d149ef"></span>
## Configure long\-term access credentials

Before initializing the SDK, configure long\-term access credentials. This section explains how to set up long\-term access credentials on different operating systems.


<Tabs>
<Tab zoneid="ON4Tvqrrxz" title="macOS">
<TabTitle>macOS</TabTitle>

1. Open Terminal and run this command to open the file.


```Shell
nano ~/.bash_profile
```



2. Add your access key ID and secret access key at the end of the file.


```Shell
export TOS_ACCESS_KEY=AKTPYmI1Z****
export TOS_SECRET_KEY=T1dJM01UU****
```



3. Save the file and exit.

4. Run this command to apply the configuration.


```Shell
source ~/.bash_profile
```



5. Run this command to verify the configuration.


```Shell
echo $TOS_ACCESS_KEY
echo $TOS_SECRET_KEY
```


The following output confirms a successful configuration.

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
<Tab zoneid="WvmBtBmwfg" title="Linux">
<TabTitle>Linux</TabTitle>

1. Open Terminal and run this command to open the file.


```Shell
sudo vim /etc/profile
```



2. Add your access key ID and secret access key at the end of the file.


```Shell
export TOS_ACCESS_KEY=AKTPYmI1Z****
export TOS_SECRET_KEY=T1dJM01UU****
```



3. Save the file and exit.

4. Run this command to apply the configuration.


```Shell
source /etc/profile
```



5. Run this command to verify the configuration.


```Shell
echo $TOS_ACCESS_KEY
echo $TOS_SECRET_KEY
```


The following output confirms a successful configuration.

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
<Tab zoneid="ZEQ5lTwta1" title="Windows">
<TabTitle>Windows</TabTitle>

1. Open the command line interface and run this command to enter your access key ID and secret access key.


```Shell
set TOS_ACCESS_KEY=AKTPYmI1Z****
set TOS_SECRET_KEY=T1dJM01UU****
```



2. Run this command to apply the configuration.


```Shell
setx TOS_ACCESS_KEY "%TOS_ACCESS_KEY%"
setx TOS_SECRET_KEY "%TOS_SECRET_KEY%"
```



3. Restart the command line interface and run this command to verify the configuration.


```Shell
echo %TOS_ACCESS_KEY%
echo %TOS_SECRET_KEY%
```


The following output confirms a successful configuration.

```Shell
AKTPYmI1Z****
T1dJM01UU****
```



</Tab>
</Tabs>


<span id="5fb21056"></span>
## Create a TosClient

After initializing the TosClient instance, you can send HTTP/HTTPS requests to the TOS service. This article describes how to initialize the Rust SDK.

TOS Rust client provides a series of interfaces to interact with TOS services for managing buckets, objects, and other TOS resources. When initializing the client, you need to provide AccessKey ID, AccessKey Secret, and Region information. During initialization, you can set optional parameters such as connection timeout, single request timeout, retry count on timeout, and maximum idle connections.

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::ListBucketsInput;
use ve_tos_rust_sdk::common::init_tracing_log;
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
    // init log
    let _guard = init_tracing_log("info", "temp/logs", "app.log");

    let ak = env::var("TOS_ACCESS_KEY").unwrap_or("".to_string());
    let sk = env::var("TOS_SECRET_KEY").unwrap_or("".to_string());
    let endpoint = "https://tos-cn-beijing.volces.com";
    let region = "cn-beijing";
    let tos_client = tos::builder::<TokioRuntime>()
        .connection_timeout(3000)
        .request_timeout(10000)
        .max_connections(1024)
        .max_retry_count(3)
        .ak(ak)
        .sk(sk)
        .region(region)
        .endpoint(endpoint)
        .build()
        .unwrap();

    let output = tos_client.list_buckets(&ListBucketsInput::new()).await;
    match output {
        Ok(output) => {
            println!("request_id: {}", output.request_id());
            for bucket in output.buckets() {
                println!("{}", bucket.name());
            }
        }
        Err(err) => {
            match err {
                TosError::TosClientError { message, .. } => {
                    println!("message: {}", message);
                }
                TosError::TosServerError { request_id, ec, .. } => {
                    println!("request_id: {}, ec: {}", request_id, ec);
                }
            }
        }
    }
}
```


<span id="ecaa06c5"></span>
## Initialization parameter list

The following parameters are supported for initializing TosClient.


|Parameter |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|ak |String |No |AKTPYmI1ZGQwMDA0NjlhNGFkMzhjNzM0N2Q0OTQ3ZTV\*\*\*\* |Access Key ID, the key ID. |
|sk |String |No |T1dJM01UUXpOak0wTVdWak5EUmtOR0poWldJNU1HWmxaV1V5TkdReVl6\*\*\*\* |SecretAccess Key, the private access key |
|endpoint |String |No |https://tos\-cn\-beijing.volces.com |The domain name accessed. |
|region |String |Yes |cn\-beijing |TOS server region. Full format: https://{host}:{port}. |
|security_token |String |No |STSeyJBY2NvdW50SWQiOjIxMDAwMDUyMjQsIklkZW50aXR5VHlwZSI6NCwiSWRlbnRpdHlJZCI6MTE3MjI5NiwiQ2hhbm5lbCI6IlVzZXIiLCJBY2Nlc3NLZXlJZCI6IkFLVFBZbUkxWkdRd01EQTBOamxoTkdGa016aGpOek0wTjJRME9UUTNaVFZqTXpFIiwiU2l\*\*\*\*\*\*\*\*\*\*\*\* |Security token in temporary access credentials. |
|control_endpoint |String |No |https://tos\-control\-cn\-beijing.volces.com |TOS server control plane domain name, full format: https://{host}:{port}. |
|enable_verify_ssl |bool |No |true |Specifies whether to verify SSL certificates. The default value is true. |
|auto_recognize_content_type |bool |No |true |Automatically detect MIME type; default is true. |
|request_timeout |isize |No |120000 |Total timeout for an HTTP request, in milliseconds. Default is 120000ms. |
|connection_timeout |isize |No |10000 |Set the connection timeout in milliseconds; default is 10,000 ms. |
|max_connections |isize |No |1024 |The maximum number of HTTP connections allowed to open in the connection pool, default is 1024. |
|idle_connection_time |isize |No |60000 |Close HTTP connection if idle time in the connection pool exceeds this parameter value, in milliseconds; default is 60000ms. |
|max_retry_count |isize |No |3 |Set the maximum retry count, the default is 3. |
|enable_crc |bool |No |true |Enable CRC check; default is true. |
|is_custom_domain |bool |No |false |Whether to prepend the bucket name to the Endpoint and access TOS via virtual host domain names. The values are as follows:<br><br><br>* `true`: do not prepend.<br><br>* `false`: prepend.<br><br><br>The default value is false.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When accessing TOS through a custom domain name, set <code>isCustomDomain</code> to <code>true</code>.</div><br> |
|proxy_host |String |No |http://your\-proxy.com |The host address of the proxy server, currently only supports the http protocol. |
|proxy_port |isize |No |8080 |Port number of the proxy server. |
|proxy_username |String |No |username |Username used when connecting to the proxy server. |
|proxy_password |String |No |password |The password used to connect to the proxy server. |
|disable_encoding_meta |bool |No |true |Whether to encode user\-defined metadata (x\-tos\-meta\-\*), Content\-Disposition; encoding is skipped when set to true, default is false |
|expect_100_continue_threshold |isize |No |65536 |When greater than 0, it indicates that the upload\-related interface enables the 100\-Continue mechanism for upload requests with data length exceeding this threshold (requests with unpredictable data length are considered above this threshold). Unit: bytes. Default is 65536. |
|high_latency_log_threshold |isize |No |100 |When greater than 0, enables high latency logs in KB. Default is 100. WARN\-level logs print when a single request's total transfer rate falls below this value and total request duration exceeds 500 ms. |
|user_agent_product_name |String |No |your\-product\-name |Business side/product name in User\-Agent extension specification. |
|user_agent_soft_name |String |No |your\-soft\-name |Software name in the User\-Agent extension specification. |
|user_agent_soft_version |String |No |v1.0.0 |Software version in the User\-Agent extension specification. |
|user_agent_customized_key_values |HashMap<String, String\> |No |\- |Custom KV key\-value pairs in the User\-Agent extension specification. |
|follow_redirect_times |isize |No |3 |Maximum number of 3xx redirects followed by Get/Head requests, default is 0, meaning no redirects are followed. |
|client_crt |String |No |\- |Client SSL certificate file path. |
|client_key |String |No |\- |Client SSL key file path. |
|ca_crt |String |No |\- |Custom root certificate file path on the server side. |


&nbsp;
