---
title: "Error InvalidPathAccess occurs when accessing TOS using PathStyle"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Error-invalidpathaccess-occurs-when-accessing-tos-using-PathStyle"
---

<span id="659fbadf"></span>
## Issue description

Error `Forbidden path to access server` or `InvalidPathAccess` occurs when accessing TOS with PathStyle request

<span id="0c8333bc"></span>
## Cause

TOS does not support PathStyle requests; it only supports [VirtualHost](https://docs.aws.amazon.com/AmazonS3/latest/userguide/VirtualHosting.html?spm=a2c4g.11186623.0.0.6b9d64012JMDoP) (VirtualHostStyle) request method

<span id="6a2e0384"></span>
## Solution

The difference between Path and VirtualHost lies primarily in the bucket name position in the HTTP URL, as shown below:

```Shell
# Path access method
https://tos-s3-cn-beijing.bytepluses.com.cn/{bucketname} 

# VirtualHost access method
https://{bucketname}.tos-s3-cn-beijing.bytepluses.com.cn
```


When accessing TOS with SDKs and tools supporting the S3 protocol, ensure the request method is configured as VirtualHostStyle For example:


* When using AWS S3 Java SDK, ensure PathStyle is disabled during client initialization with the parameter `AmazonS3Builder.withPathStyleAccessEnabled(false)`

* When using the AWS CLI tool to access TOS, add `addressing_style = virtual` in the `~/.aws/config` file to ensure the request uses VirtualHostStyle.
