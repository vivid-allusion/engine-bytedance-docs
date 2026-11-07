---
title: "Calling method"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/calling-method"
---

ByteHouse OpenAPI uses Bearer Token authorization. You must create and use an API Key as a secret on the [ByteHouse Console](https://console.byteplus.com/bytehouse/region:bytehouse+ap-southeast-1/tenant/connection).

<span id="ac868849"></span>
### Obtain the OpenAPI address

On the Console, go to **Tenant Management** \> **Connection Information** page, you can obtain the OpenAPI connection address (private or public network).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/051a8b68e38e42f99a7572b67df4142f~tplv-goo7wpa0wc-image.image) </span>

<span id="fa9f380e"></span>
### **Obtain** API **Key**

In the tenant management\-connection information page, click the "New" button under the API Key form to create an API Key.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">API Key <strong>cannot be viewed again after creation</strong>, it is recommended to download and save the key locally.</div>


* <div data-tips="true" data-tips-type="warning">A maximum of 2 API Keys can be created.</div>


* <div data-tips="true" data-tips-type="warning">The key needs to be refreshed within 90 days to ensure security.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34a4f5bf2c844cae8ccd76b4e426c430~tplv-goo7wpa0wc-image.image) </span>

<span id="e98cac36"></span>
### Obtain API interface

You can refer to [API List](https://docs.byteplus.com/docs/bytehouse/api-list) to obtain the corresponding interface.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Due to interface optimization, when using the Queries\-V2 interface, the port number "8123" needs to be added to the URL.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb6f0571afbe4146a1eb8f1b9e61ca69~tplv-goo7wpa0wc-image.image" width="654px" /></div>


<span id="1859dfa9"></span>
#### Example

For specific API usage, refer to the interface documentation of different modules. Examples are as follows:


|Use the Queries\-V2 interface |Use the Queries\-V1 interface |
|---|---|
|```Shell```<br>```curl --request POST \```<br>``` --url https://{OPENAPI_HOST}:8123/v2/sql/sync \```<br>``` --header 'accept: application/json' \```<br>``` --header 'authorization: Bearer ${API_KEY}' \```<br>``` --header 'content-type: application/json' \```<br>``` --data '```<br>```{```<br>``` "mode": "ansi_sql",```<br>``` "query": "select 1"```<br>```}```<br>```'```<br> |```Shell```<br>```curl --request POST \```<br>``` --url https://{OPENAPI_HOST}/v1/sql/sync \```<br>``` --header 'accept: application/json' \```<br>``` --header 'authorization: Bearer ${API_KEY}' \```<br>``` --header 'content-type: application/json' \```<br>``` --data '```<br>```{```<br>``` "mode": "ansi_sql",```<br>``` "query": "select 1"```<br>```}```<br>```'```<br> |



* POST: Represents the request method for ByteHouse OpenAPI.

* URL: Specifies the address for accessing OpenAPI, which includes parameters such as region. If using the Queries\-V2 interface, the URL must include port number 8123.

* HTTPS: Specifies the communication protocol for the request.
