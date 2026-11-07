---
title: "Initializing client"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Initializing_client"
---

The DTS Go SDK supports initializing the client through a Session. A DTS client created through a session reuses underlying HTTP/HTTPS resources (connections or requests). When you need to initialize multiple clients for operations, creating them through a session can improve client performance. This topic describes how to initialize the client through a session.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The DTS Go SDK has been downloaded and installed. For specific steps, refer to [Downloading and installing SDK](https://docs.byteplus.com/en/docs/DTS/Downloading_and_installing_the_SDK).

* Before initializing the client, make sure that you have obtained the following information:

   * The Access Key ID (AK) and Secret Access Key (SK) information of the account. For instructions on how to obtain AKSK information, refer to [Viewing AKSK information](https://docs.byteplus.com/en/docs/6291/65568).

   * Region information. For the Regions supported by DTS, refer to [Service address](https://docs.byteplus.com/en/docs/DTS/request_structure#.5pyN5Yqh5Zyw5Z2A).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initialize client

DT) supports two AK and SK configuration methods. During verification and testing phases, you can configure AK and SK in the Demo. If you need to publish to the production environment, configure AK and SK in the environment variables.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">During the call, the system automatically reads the configuration parameters. The AK and SK priorities configured in the debug code are higher than the configuration in environment variables.</div>


<span id=".5Zyo546v5aKD5Y-Y6YeP5Lit6YWN572uLWFrLeWSjC1zaw=="></span>
### Configure AK and SK in environment variables

Select a method to configure AK and SK based on your operating system.


* **Linux or macOS operating system**

   Execute the command below in the terminal with the prepared AK and SK.

   ```plaintext
   export VOLC_ACCESSKEY="ak"
   export VOLC_SECRETKEY="sk"
   ```
   

* **Windows operating system**

   Create a new system environment variable. Add the environment variables VOLC_ACCESSKEY and VOLC_SECRETKEY, then provide your prepared AK and SK.


<span id=".5Zyo6LCD6K-VLWRlbW8t5Lit6YWN572uLWFrLeWSjC1zaw=="></span>
### Configure AK and SK in the Demo

This method poses potential security risks. Therefore, do not configure AK/SK in plaintext for production environments.

Provide AK and SK parameters with each call to DTS\-related functions, suitable for rapid validation and testing.

```go
instance := dts_v20221001.NewInstance()
instance.SetCredential(base.Credentials{
        AccessKeyID: "ak",
        SecretAccessKey: "sk",
})
```
