---
title: "Configure timeout and retry strategies (iOS SDK legacy)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_ios_retry_policy"
---

This document describes how to adjust the timeout duration and retry strategies through Client configuration.

## Set the request timeout duration

You can set the timeout duration in milliseconds in the Client configuration. If the server does not respond within the specified duration, the SDK will return immediately and provide an empty response.

The following example shows how to configure a request timeout of 100 milliseconds.

```objectivec
TLSClientConfig *config = [TLSClientConfig alloc]; {
        config.endpoint = @"XXXX";
        config.region = @"XXXX";
        config.accessKeyId = @"XXXX";
        config.accessKeySecret = @"XXXX";
        config.timeoutMillisecond = [[NSNumber alloc] initWithInt:100];
    }
    TLSClient *client = [[TLSClient alloc] initWithConfig:config];
```

## Configure SDK retries

By default, the TLS iOS SDK includes a built\-in retry mechanism for HTTP errors such as 429 and 500, which is enabled by default. To disable the retry mechanism, configure disableRetry in the config.

```objectivec
TLSClientConfig *config = [TLSClientConfig alloc]; {
        config.endpoint = @"XXXX";
        config.region = @"XXXX";
        config.accessKeyId = @"XXXX";
        config.accessKeySecret = @"XXXX";
        config.disableRetry = true;
    }
    // Make client
    TLSClient *client = [[TLSClient alloc] initWithConfig:config];
```
