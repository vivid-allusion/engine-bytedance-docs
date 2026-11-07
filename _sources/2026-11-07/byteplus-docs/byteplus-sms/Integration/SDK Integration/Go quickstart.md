---
title: "Go quickstart"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-go-quickstarts"
---

Use BytePlus SDK for Go to call SendSms API so that you can send a text message to a group of recipients by using an example file.

<span id="34d4f410"></span>
## Prerequisites


* Go 1.13.1 or later

* Have generated AK (Access Key) and SK (Secret Key).

   If you haven't generated AK/SK yet, go to [BytePlus Console](https://console.byteplus.com/auth/login/) \> **User Profile** \> **IAM** \> **Key Management** \> **Create New Access Key**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each BytePlus account can have maximum 2 pairs of AK/SK at the same time.   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/336d25c-AKSK.png) </span>


<span id="b5958e0b"></span>
## Downloading SDK for Go

The SDK for Go provides an example project file called [demo_sms_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/tree/master/example/demo_sms) for you to quickly call SendSms API.

To download the SDK, follow the steps:


1. Go to [BytePlus SDK for Go](https://github.com/byteplus-sdk/byteplus-sdk-golang).

2. In the upper right corner, click **Code** \> **Download ZIP**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/fa6a4d7-Go.png) </span>


<span id="5bdc264a"></span>
## Installing the SDK

Run the following code in the terminal window to install BytePlus SDK for Go.

```go
go get -u github.com/byteplus-sdk/byteplus-sdk-golang@latest
```


Setting up authentication

Open the example file [demo_sms_test.go](https://github.com/byteplus-sdk/byteplus-sdk-golang/tree/master/example/demo_sms).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This is the recommended way to set up authentication.</div>


```go
testAk = "testAK"
testSk = "testSk"
```


Alternatively, you can also fulfill your AK and SK in the environment variable setting as shown below.

```go
BYTEPLUS_ACCESSKEY="your ak"  
BYTEPLUS_SECRETKEY="your sk"
```


Otherwise, you can fulfill your AK and SK by creating a JSON file under ～/.byteplus/config as shown below.

```go
{"ak":"your ak","sk":"your sk"}
```


<span id="c5f8ac0f"></span>
## Sending text messages using SendSms API


1. Fulfill the parameters in the body section of the example file **demo_sms_test.go** as shown below. To understand the parameters, refer to [SendSms](https://docs.byteplus.com/byteplus-sms/docs/sendsms).


```go
package demo_sms

import (
   "encoding/json"
   "testing"

   "github.com/byteplus-sdk/byteplus-sdk-golang/base"
   "github.com/byteplus-sdk/byteplus-sdk-golang/service/sms"
)

const (
   testAk = "AK0000"
   testSk = "SK0000"
)

type ParamStruc struct {
   Code string `json:"code"`
   Time string `json:"time"`
}

func TestSMS_sendI18n(t *testing.T) {
   i18nInstance := sms.NewInstanceI18n(base.RegionApSingapore)
   i18nInstance.Client.SetAccessKey(testAk)
   i18nInstance.Client.SetSecretKey(testSk)
   c := ParamStruc{Code: "43133", Time:"10"}
   cj, _ := json.Marshal(c)
   req := &sms.SmsRequest{
      SmsAccount:    "19cb0000",
      From:          "BytePlus",
      TemplateID:    "SPT_1ba0000",
      TemplateParam: string(cj),
      PhoneNumbers:  "+6500000000",
      Tag:           "tag",
   }
   result, statusCode, err := i18nInstance.Send(req)
   t.Logf("result = %+v\n", result)
   t.Logf("statusCode = %+v\n", statusCode)
   t.Logf("err = %+v\n", err)
}
```



2. In the terminal window, run the following command.


```go
go test -v example/demo_sms/demo_sms_test.go
```


<span id="46f7c56e"></span>
## Result

After the text message is sent, you will receive a success message containing a MessageID in the response.
