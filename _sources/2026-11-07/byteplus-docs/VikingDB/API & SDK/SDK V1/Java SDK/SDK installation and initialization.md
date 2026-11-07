---
title: "SDK installation and initialization"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/SDK_installation_and_initialization"
---

<span id="sdk-installation-and-initialization"></span>
# SDK installation and initialization

Before you can use the Java SDK to interact with Vector Database, you need to set up your development environment. This guide provides step\-by\-step instructions on how to add the SDK as a Maven dependency and initialize the database client with your credentials and service endpoint.

<span id="60c6ad04"></span>
# Prerequisites


1. You have [registered an account and enabled the related service](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

2. You have obtained the access key for BytePlus. The access key consists of an access key ID and a secret access key. You can log in to the BytePlus console and go to the Key management page to view the access key ID and secret access key of the current account. For more information, refer to [Access key management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).


<span id="66072615"></span>
# Install the SDK

It is recommended that you use the BytePlus SDK for Java through Maven dependencies.

```Java
 <dependency> 
    <groupId>com.volcengine</groupId> 
    <artifactId>volc-sdk-java</artifactId> 
    <version>Latest version</version> 
</dependency>
```


You can find the latest version number in the ["Obtain and install the SDK" section in the README file at GitHub](https://github.com/volcengine/volc-sdk-java?tab=readme-ov-file), as shown in the figure on the right.

You can directly copy the latest version number, such as 1.0.206, in this section to your code.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8af7f427b91e44518430fa4bb338cd1f~tplv-goo7wpa0wc-image.image) </span>

<span id="1bf42ec5"></span>
# Initialize the SDK

Configure the access key and initialize the client based on the vector database name and tokens. The domain name (specified by the host parameter) supports both HTTP and HTTPS protocols. You can choose either of them as needed.


* Domain name for Hong Kong: [api-vikingdb.mlp.cn-hongkong.bytepluses.com](http://api-vikingdb.mlp.cn-hongkong.bytepluses.com/)

* Domain name for Johor: api\-vikingdb.mlp.ap\-mya.byteplus.com


You can configure the region parameter as required, such as **cn\-hongkong and ap\-southeast\-1** for Hong Kong and Johor, respectively.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the sample code, you need to replace Your ak, Your sk, Your host, Your region, and Your scheme with the actual access key ID, access secret key, domain name, region, and request protocol.</div>


```Java
import com.volcengine.service.vikingDB.Collection; 
import com.volcengine.service.vikingDB.Index; 
import com.volcengine.service.vikingDB.VikingDBService; 
import com.volcengine.service.vikingDB.common.*; 

public class test { 
 public static void main(String[] args) throws Exception { 
 // You do not need to include the protocol (like http:// or https://) in the host parameter. 
 // When the schema is http, you can set the host name to either an IP address or a domain name. When the schema is https, you can set the host name only to a domain name. 
 // The schema parameter is optional. The valid values are http (default value) and https. 
 VikingDBService vikingDBService = new VikingDBService("Your host", "Your region", "Your ak", "Your sk", "Your scheme"); 
 } 
}
```
