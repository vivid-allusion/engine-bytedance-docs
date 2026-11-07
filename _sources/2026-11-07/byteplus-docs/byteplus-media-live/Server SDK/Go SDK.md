---
title: "Go SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-golang-sdk"
---

This article introduces how to install the Go SDK and provides code examples to help you accelerate your development process.

<span id="b4fa9856"></span>
## **Prerequisites**


* Access key, refer to [Server SDK overview](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk#get-access-key).

* Environmental requirements: Go 1.13 or higher is required. For instructions to download and install the Go compilers, tools, and libraries, view the [install documentation](https://go.dev/doc/install).


<span id="9ee0aef8"></span>
## Installing or Upgrade the SDK

In terminal, run the following command to install the latest version of the Go SDK:

```Python
go get github.com/byteplus-sdk/byteplus-sdk-golang
```


In terminal, run the following command to upgrade the current version to the latest version of the Go SDK:

```Groovy
go get -u github.com/byteplus-sdk/byteplus-sdk-golang
```


<span id="fe00307b"></span>
### Setting the Access key

To set the **Access Key ID** and **Secret Access Key**, you can use either of the following methods:


* Set the environment variables `BYTEPLUS_ACCESSKEY` as **Access Key ID** and `BYTEPLUS_SECRETKEY` as **Secret Access Key**.

* Pass the **Access Key ID** and **Secret Access Key** when calling the API. The code sample is as follows:

   ```Go
   instance := live_v20230101.NewInstance()
   instance.SetCredential(base.Credentials{
           AccessKeyID: "Access Key ID",
           SecretAccessKey: "Secret Access Key",
   })
   ```
