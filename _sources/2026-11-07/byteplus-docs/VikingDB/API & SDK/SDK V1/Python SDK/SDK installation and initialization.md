---
title: "SDK installation and initialization"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/SDK_installation_and_initialization1"
---

<span id="sdk-installation-and-initialization"></span>
# SDK installation and initialization

To begin interacting with Vector Database from your Python application, you must first set up the SDK. This guide provides the necessary steps to install the SDK using pip and initialize the client with your access credentials, region, and host information, preparing your environment for development.

<span id="94e0bae9"></span>
# Prerequisites


1. You have [registered an account and enabled the related service](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

2. You have obtained the access key for BytePlus. The access key consists of an access key ID and a secret access key. You can log in to the BytePlus console and go to the Key management page to view the access key ID and secret access key of the current account. For more information, refer to [Access key management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).


<span id="e89d14fc"></span>
# Install the SDK

You can use pip to install the SDK for Python 3.7 and later versions before first use.

```Python
pip install --user volcengine
```


You can run the following command to update the SDK:

```Python
pip install --upgrade volcengine
```


<span id="c1747fce"></span>
# Initialize the SDK

Configure the access key and initialize the client based on your connection details. The domain name (specified by the host parameter) supports both HTTP and HTTPS protocols. You can choose either of them as needed.


* Domain name for Hong Kong: [api-vikingdb.mlp.cn-hongkong.byteplus.com](http://api-vikingdb.mlp.cn-hongkong.bytepluses.com/)

* Domain name for Johor: api\-vikingdb.mlp.ap\-mya.byteplus.com

* If you access VikingDB on a private network, you can configure and obtain the domain name by referring to [Access VikingDB on a private network](https://www.volcengine.com/docs/84313/1254445). Currently, private network access supports only the HTTP protocol.


You can configure the region parameter as required, such as **cn\-hongkong for Hong Kong and ap\-southeast\-1 for Johor**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the sample code, you need to replace Your ak, Your sk, Your host, Your region, and Your scheme with the actual access key ID, access secret key, domain name, region, and request protocol.</div>


```Python
from volcengine.viking_db import * 
# You do not need to include the protocol (like http:// or https://) in the host parameter. 
# When the schema is http, you can set the host name to either an IP address or a domain name. When the schema is https, you can set the host name only to a domain name. 
# The schema parameter is optional. The valid values are http (default value) and https. 
# You can configure the connection_timeout parameter as needed. The default value is 30s. 
# You can configure the socket_timeout parameter as needed. The default value is 30s. 
vikingdb_service = VikingDBService(host="Your host", region="Your region", scheme="Your scheme",connection_timeout=30, socket_timeout=30) 
vikingdb_service.set_ak("Your ak") 
vikingdb_service.set_sk("Your sk")
```
