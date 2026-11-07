---
title: "Java quickstart"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-java-quickstarts"
---

Use BytePlus SDK for Java to call SendSms API so that you can send a text message to a group of recipients by using an example file.

<span id="32f3fb1d"></span>
## Prerequisites


* Maven is integrated.

   Maven is a powerful tool that allows you to import dependencies into your software projects and also automatically manage transitive dependencies.

* Have generated AK (Access Key) and SK (Secret Key).

   If you haven't generated AK/SK yet, go to [BytePlus Console](https://console.byteplus.com/auth/login/) \> **User Profile** \> **IAM** \> **Key Management** \> **Create New Access Key**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each BytePlus account can have maximum 2 pairs of AK/SK at the same time.   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/bb3defe-AKSK.png) </span>


<span id="07cc53d5"></span>
## Downloading SDK for Java

The SDK for Java provides an example project file called [SendSmsDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/tree/master/example/src/main/java/com/byteplus/example/sms) for you to quickly call SendSms API.

To download the SDK, follow the steps:


1. Go to [BytePlus SDK for Java](https://github.com/byteplus-sdk/byteplus-sdk-java).

2. In the upper right corner, click **Code** \> **Download ZIP**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/5e7acb4-Java.png) </span>


<span id="1a6a1b07"></span>
## Add dependency to Maven pom.xml file

In your IDE, open the example folder in the SDK as a Maven project. The following Maven dependency has been added to the [pom.xml](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/pom.xml) file, so you don't have to add it again. But if you would like to integrate the SDK with your own project, this step is required. Once added to the Maven pom.xml file, dependencies will be automatically downloaded, updated, and have their sub\-dependencies managed by Maven.

```java
<dependency>
    <groupId>com.byteplus</groupId>
    <artifactId>byteplus-sdk-java</artifactId>
    <version>latest</version>
</dependency>
```


Setting up authentication

Open the example file [SendSmsDemo.java](https://github.com/byteplus-sdk/byteplus-sdk-java/tree/master/example/src/main/java/com/byteplus/example/sms).

To set up authentication by AK/SK, fulfill your AK and SK in the example file as shown below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This is the recommended way to set up authentication.</div>


```java
smsService.setAccessKey("ak");
smsService.setSecretKey("sk");
```


Alternatively, you can also fulfill your AK and SK in the environment variable setting as shown below.

```java
BYTEPLUS_ACCESSKEY="your ak"  
BYTEPLUS_SECRETKEY="your sk"
```


Otherwise, you can fulfill your AK and SK by creating a JSON file under ～/.byteplus/config as shown below.

```java
{"ak":"your ak","sk":"your sk"}
```


<span id="5f2a964c"></span>
## Sending text messages using SendSms API


1. Fulfill the parameters in the body section of the example file **SendSmsDemo.java** as shown below. To understand the parameters, refer to [SendSms](https://docs.byteplus.com/byteplus-sms/docs/sendsms).


```java
package com.byteplus.example.sms;

import com.alibaba.fastjson.JSON;
import com.byteplus.model.request.SmsSendRequest;
import com.byteplus.model.response.SmsSendResponse;
import com.byteplus.service.sms.SmsService;
import com.byteplus.service.sms.impl.SmsServiceImpl;

public class SendSmsDemo {

    public static void main(String[] args) throws Exception {
        SmsService smsService = SmsServiceImpl.getInstance("ap-singapore-1");

        // call below method if you dont set ak and sk in ～/.vcloud/config
        smsService.setAccessKey("AK0000");
        smsService.setSecretKey("SK0000");

        SmsSendRequest req = new SmsSendRequest();
        req.setFrom("BytePlus");
        req.setSmsAccount("19cb0000");
        req.setPhoneNumbers("+6500000000");
        req.setTemplateId("SPT_1ba0000");
        req.setTemplateParam("{\"code\":\"36440\",\"time\":\"10\"}");
        req.setTag("tag");
        try {
            SmsSendResponse response = smsService.send(req);
            System.out.println(JSON.toJSONString(response));
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```



2. Right click and run Java.


<span id="b554c4ac"></span>
## Result

After the text message is sent, you will receive a success message containing a MessageID in the response.
