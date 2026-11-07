---
title: "Install and initialize the Go SDK"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Go_installation_and_initialization"
---

This guide shows you how to download, install, and initialize the Go SDK for the LLM Application Firewall. By following these steps, you can quickly configure a client instance in your Go project, enabling you to start protecting your LLM applications.

<span id="3b8e665d"></span>
## Prerequisites


* Obtain the Access Key ID (AK) and Secret Access Key (SK). You have two options:

   * Go to [BytePlus IAM > Access key management](https://console.byteplus.com/iam/keymanage) to find your existing access key pair.

   * Create a RAM user and generate a new AccessKey pair. For details, refer to [Create a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

* In the LLM Application Firewall console, add an asset and configure its protection policies. For details, refer to [Introduction to protection policies](https://docs.byteplus.com/docs/LLM-Application-Firewall/introduction_to_protection_policy).


&nbsp;

<span id="14d11b06"></span>
## Environment requirements

Go 1.5 or later is required. We recommend Go 1.12 or later.

<span id="ba4239fa"></span>
## Download the SDK

Use the command below to download the SDK.

```Bash
go get github.com/byteplus-sdk/byteplus-go-sdk-v2
```


<span id="1470746a"></span>
## Initialization

The following describes the initialization parameters and the corresponding sample code.

<span id="2d7a8ad9"></span>
### Parameter description


|Parameter |Example |Description |
|---|---|---|
|myUrl |https://ap\-southeast\-1.sdk.access\-bp.llm\-shield.omni\-shield.ai<br><br> |* **Parameter description**: The endpoint for the LLM Application Firewall service has the format **`https://`**  **`{region}`**  **`.sdk.access-bp.llm-shield.omni-shield.ai`**, where {region} is the region of your provisioned instance.<br><br>   * ap\-southeast\-1<br><br>   * cn\-hongkong<br><br>* **Finding this value**: You can find the region in the instance management module of the LLM Application Firewall console. |
|ak, sk |* AK : AKLTYWRhNDMw\*\*\*\*<br><br>* SK: TWprNE5XVXlZbc\*\*\*\* |These are the **Access Key ID** and **Secret Access Key** for your BytePlus account. |
|appid |app\-d35p9du8pa51\*\*\*\* |* **Parameter description**: The unique identifier of the asset. After you add an asset in the console, the system automatically generates an AppID.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When making SDK calls, only assets integrated via the SDK method are supported.   </div><br>   <br><br>* **Finding this value**: Go to the asset management module in the LLM Application Firewall console to view the AppIDs of assets integrated via SDK. |
|region |ap\-southeast\-1 |* **Parameter description**: This is the region of your LLM Application Firewall instance. It must match the region specified in `myUrl`.<br><br>   * ap\-southeast\-1<br><br>   * cn\-hongkong<br><br>* **Finding this value**: Go to the LLM Application Firewall console instance management module to view the region where the instance is located. |


&nbsp;

&nbsp;

<span id="a9740652"></span>
### Sample code

The following example shows the complete initialization code:

```Go
package main

import (
    "fmt"
    "time"
    "github.com/byteplus-sdk/byteplus-go-sdk-v2/service/llmshield"
)

func main() {
        var err error
        // Replace the parameters with the actual values
        myUrl := "https://ap-southeast-1.sdk.access-bp.llm-shield.omni-shield.ai" // Endpoint of your LLM Application Firewall instance
        ak := "YOUR AK"   // Access key of your BytePlus account
        sk := "YOUR SK"   // Secret key of your BytePlus account
        appid := "app-d45gff4r7odm2ols****"  // The AppID for your asset, which can be found in the console
        region := "ap-southeast-1"   // Region of the LLM Application Firewall instance
        timeout := time.Second * 30  // Timeout (seconds)

        // Create a client instance
        client := llmshield.New(myUrl, ak, sk, region, timeout)
```
