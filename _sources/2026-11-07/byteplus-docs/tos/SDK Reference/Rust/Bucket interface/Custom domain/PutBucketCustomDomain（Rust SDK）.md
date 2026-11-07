---
title: "PutBucketCustomDomain（Rust SDK）"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutBucketCustomDomain"
---

The put_bucket_custom_domain interface binds a custom domain name to a bucket. This article explains how to bind it using the put_bucket_custom_domain interface in the Rust SDK. After binding, you must point the domain's CNAME to the bucket's external network domain name.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You need to fill in the region and access domain in the sample code according to your actual situation. For details, see [Region and Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* To prevent key leakage, the sample code reads the Access Key ID and Secret Access Key from environment variables. Therefore, before using the SDK, configure long\-term access credentials. For details, see [Configure Long-term Access Credentials](https://docs.byteplus.com/docs/tos/Initialize_the_client_Rust_SDK#b0d149ef).

* Each bucket can hold up to 20 bound custom domain names. If exceeded, put_bucket_custom_domain returns an error.

* The `domain` field in the request body must be a domain name that has passed ICP filing; otherwise, put_bucket_custom_domain will not take effect.

* If `cert_id` is empty, put_bucket_custom_domain uses the HTTP protocol; if `cert_id` is provided, the system enforces HTTPS and verifies the certificate's validity.


<span id=".5p2D6ZmQ6K-05piO"></span>
## Permissions required

The BytePlus main account has all permissions by default, but IAM users have no permissions by default. If you need to use a sub\-account to perform the put_bucket_custom_domain operation, the BytePlus main account must grant the following permissions to the sub\-account through [IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6) and [bucket policies](https://docs.byteplus.com/docs/tos/docs-overview_5):

tos:PutBucketCustomDomain

<span id=".5Luj56CB56S65L6L"></span>
## Code example

<span id=".5Li65a2Y5YKo5qG257uR5a6a6Ieq5a6a5LmJ5Z-f5ZCN"></span>
### Bind a custom domain to a bucket

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::sync::Arc;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::{CustomDomainRule, PutBucketCustomDomainInput};
use ve_tos_rust_sdk::enumeration::AuthProtocolType;

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

    // Create custom domain rules
    let rule = CustomDomainRule::new("example.com", AuthProtocolType::AuthProtocolTos);
    
    // Create input parameters
    let input = PutBucketCustomDomainInput::new("my-bucket", rule);
    
    // Call the API and bind a custom domain
    let output = client.put_bucket_custom_domain(&input).await;
    
    match output {
        Ok(output) => {
            println!("Custom domain binding successful，Request ID: {}", output.request_id());
        }
        Err(err) => {
            eprintln!("Custom domain binding failed: {:?}", err);
        }
    }
}
```


<span id=".5Li65a2Y5YKo5qG26K6-572u5aSa5p2h6Ieq5a6a5LmJ5Z-f5ZCN"></span>
### Set multiple custom domains for a bucket

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::sync::Arc;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::{CustomDomainRule, PutBucketCustomDomainInput};
use ve_tos_rust_sdk::enumeration::AuthProtocolType;

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

    // Define multiple domain configurations
    let domains = vec![
        ("domain1.com", AuthProtocolType::AuthProtocolTos, ""),
        ("domain2.com", AuthProtocolType::AuthProtocolS3, "cert-1234567890"),
        ("domain3.com", AuthProtocolType::AuthProtocolTos, ""),
    ];
    
    for (domain, protocol, cert_id) in domains {
        // Create custom domain rules
        let mut rule = CustomDomainRule::new(domain, protocol);
        
        // If a certificate ID is available, then set it
        if !cert_id.is_empty() {
            rule.set_cert_id(cert_id);
        }
        
        // Create input parameters
        let input = PutBucketCustomDomainInput::new("my-bucket", rule);
        
        // Call the API and bind a custom domain
        let output = client.put_bucket_custom_domain(&input).await;
        
        match output {
            Ok(output) => {
                println!("Domain name {} successfully bound, Request ID: {}", domain, output.request_id());
            }
            Err(err) => {
                eprintln!("Domain name {} binding failed: {:?}", domain, err);
            }
        }
    }
}
```


<span id=".5Li66Ieq5a6a5LmJ5Z-f5ZCN6K6-572u6K-B5LmmLWlk"></span>
### Set certificate ID for a custom domain

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::sync::Arc;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::{CustomDomainRule, PutBucketCustomDomainInput};
use ve_tos_rust_sdk::enumeration::AuthProtocolType;

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

    // Create custom domain rules
    let mut rule = CustomDomainRule::new("secure-domain.com", AuthProtocolType::AuthProtocolTos);
    
    // Set Certificate ID
    rule.set_cert_id("cert-***");
    
    // Create input parameters
    let input = PutBucketCustomDomainInput::new("my-bucket", rule);
    
    // Call the API and bind a custom domain
    let output = client.put_bucket_custom_domain(&input).await;
    
    match output {
        Ok(output) => {
            println!("Custom domain name with certificate successfully bound, request ID: {}", output.request_id());
        }
        Err(err) => {
            eprintln!("Custom domain binding with certificate failed: {:?}", err);
        }
    }
}
```


<span id=".5L2_55SoLXMzLeWNj-iurue7keWumuiHquWumuS5ieWfn-WQjQ=="></span>
### Bind a custom domain using the S3 protocol

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::sync::Arc;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::{CustomDomainRule, PutBucketCustomDomainInput};
use ve_tos_rust_sdk::enumeration::AuthProtocolType;

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

    // Create custom domain rules using the S3 protocol
    let rule = CustomDomainRule::new("s3-domain.com", AuthProtocolType::AuthProtocolS3);
    
    // Create input parameters
    let input = PutBucketCustomDomainInput::new("my-bucket", rule);
    
    // Call the API and bind a custom domain
    let output = client.put_bucket_custom_domain(&input).await;
    
    match output {
        Ok(output) => {
            println!("S3 protocol custom domain binding successful, requesting ID: {}", output.request_id());
        }
        Err(err) => {
            eprintln!("S3 protocol custom domain binding failed: {:?}", err);
        }
    }
}
```


<span id=".5L2_55SoLXRvcy3ljY_orq7nu5Hlrproh6rlrprkuYnln5_lkI0="></span>
### Bind a custom domain using the TOS protocol

```Rust
use async_trait::async_trait;
use futures_core::future::BoxFuture;
use std::env;
use std::future::Future;
use std::sync::Arc;
use std::time::Duration;
use tokio::runtime::Handle;
use ve_tos_rust_sdk::asynchronous::bucket::BucketAPI;
use ve_tos_rust_sdk::asynchronous::tos;
use ve_tos_rust_sdk::asynchronous::tos::AsyncRuntime;
use ve_tos_rust_sdk::bucket::{CustomDomainRule, PutBucketCustomDomainInput};
use ve_tos_rust_sdk::enumeration::AuthProtocolType;

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
        .build()
        .unwrap();

    // Create custom domain rules using the TOS protocol
    let rule = CustomDomainRule::new("my-domain.com", AuthProtocolType::AuthProtocolTos);

    // Create input parameters
    let input = PutBucketCustomDomainInput::new("my-bucket", rule);

    // Call the API and bind a custom domain
    let output = client.put_bucket_custom_domain(&input).await;

    match output {
        Ok(output) => {
            println!(
                "TOS protocol custom domain binding successful, requesting ID: {}",
                output.request_id()
            );
        }
        Err(err) => {
            eprintln!("TOS protocol custom domain binding failed: {:?}", err);
        }
    }
}

```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For the API documentation on PutBucketCustomDomain, see [PutBucketCustomDomain](https://docs.byteplus.com/docs/tos/Putbucketcustomdomain).
