---
title: "Configure timeout and retry policies"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_c_retry_policy"
---

This topic describes how to configure the client to adjust the timeout period and retry policy.

<span id="设置请求超时时长"></span>
## Setting the request timeout period

In client configurations, set the timeout period of a request in milliseconds. If the specified period is reached but the server does not respond, the SDK returns an empty response.

The following sample code sets the request timeout period to 100 milliseconds.

```cpp
TlsClientConfig cfg; {
        // Create client
        cfg.scheme = "http://";
        cfg.endpoint = "Your endpoint";
        cfg.access_key_id = "Your access key";
        cfg.access_key_secret = "Your access key secret";
        cfg.region = "Your region";
        cfg.timeout_millisecond = 100;
    }
    TlsClient client = TlsClient(cfg);
```


<span id="配置-sdk-重试"></span>
## Configuring the SDK retry policy

Torch Log Service (TLS) SDK for C++ has a built\-in retry mechanism for HTTP error codes such as 429 and 500, and the mechanism is enabled by default. To disable the retry mechanism, set cfg.disable_retry to true.

```cpp
TlsClientConfig cfg; {
        // Create client
        cfg.scheme = "http://";
        cfg.endpoint = "Your endpoint";
        cfg.access_key_id = "Your access key";
        cfg.access_key_secret = "Your access key secret";
        cfg.region = "Your region";
        cfg.disable_retry = true;
    }
    TlsClient client = TlsClient(cfg);
```
