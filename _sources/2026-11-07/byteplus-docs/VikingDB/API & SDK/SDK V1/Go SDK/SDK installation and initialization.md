---
title: "SDK installation and initialization"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/gosdk_SDK_installation_and_initialization"
---

<span id="sdk-installation-and-initialization"></span>
# SDK installation and initialization

To begin interacting with VikingDB using Go, you must first install the SDK and initialize a client. This guide provides the necessary commands and code samples to configure your access credentials and create a client instance, enabling you to start performing operations in your database.

<span id="46acf2c8"></span>
# Prerequisites


1. You have [registered an account and enabled the related service](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

2. You have obtained the access key for BytePlus. The access key consists of an access key ID and a secret access key. You can log in to the BytePlus console and go to the Key management page to view the access key ID and secret access key of the current account. For more information, refer to [Access key management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).


<span id="47a81747"></span>
# Install the SDK

Install the SDK for Go 1.14 and later versions.

```Go
    go get -u github.com/volcengine/volc-sdk-golang
```


<span id="cbe60a74"></span>
# Initialize the SDK

Configure the access key and initialize the client based on the vector database name and tokens. The domain name (specified by the host parameter) supports both HTTP and HTTPS protocols. You can choose either of them as needed.


* Domain name for Hong Kong: [api-vikingdb.mlp.cn-hongkong.bytepluses.com](http://api-vikingdb.mlp.cn-hongkong.bytepluses.com/)

* Domain name for Johor: api\-vikingdb.mlp.ap\-mya.byteplus.com

* If you access VikingDB on a private network, you can configure and obtain the domain name by referring to [Access VikingDB on a private network](https://www.volcengine.com/docs/84313/1254445). Currently, private network access supports only the HTTP protocol.


You can configure the region parameter as required. For example, use **cn\-hongkong** for Hong Kong and **ap\-southeast\-1** for Johor.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the sample code, you need to replace Your ak, Your sk, Your host, Your region, and Your scheme with the actual access key ID, access secret key, domain name, region, and request protocol.</div>


```Go
import ( 
        "github.com/volcengine/volc-sdk-golang/service/vikingdb" 
) 
func main() { 
        // You do not need to include the protocol (like http:// or https://) in the host parameter. Instead, specify this information in the scheme parameter. 
        // When the scheme is http, you can set the host name to either an IP address or a domain name. When the scheme is https, you can set the host name only to a domain name. 
        // The scheme parameter is optional. The valid values are http (default value) and https. 
        service := vikingdb.NewVikingDBService("Your host", "Your region", "Your ak", "Your sk", "Your scheme") 
}
```


(Optional) Configure connectionTimeout

```Go
// The default value of connectionTimeout is 5s. You can configure this parameter as needed. 
service.SetConnectionTimeout(5)
```
