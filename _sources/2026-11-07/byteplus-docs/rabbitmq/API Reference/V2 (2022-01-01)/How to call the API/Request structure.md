---
title: "Request structure"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Request_structure"
---

This section introduces the composition of API requests for Message Queue for RabbitMQ.

<span id=".6K-35rGCVVJM"></span>
## Request URL

You can call the Message Queue for RabbitMQ API service by sending an HTTPS POST request. The format of the HTTPS request URL is as follows:

```plaintext
POST {URI-scheme}://{Endpoint}/?Action={Action}&Version={Version} HTTP/1.1
```


The components are:


* URI\-scheme: Indicates the protocol used to transmit the request. Currently, all APIs use the HTTPS protocol.

* Endpoint: Specifies the server domain name or IP that hosts the service endpoint, i.e., the service address. The endpoint for Message Queue for RabbitMQ is `rabbitmq.byteplusapi.com`. For details, refer to the [service address](https://docs.byteplus.com/en/docs/rabbitmq/Service_address).

* Action: The action to execute. Enter the name of the API interface to be called here. For the Message Queue for RabbitMQ API interface, please refer to the [API Overview](https://docs.byteplus.com/en/docs/rabbitmq/API_overview).

* Version: API version number in `YYYY-MM-DD` format. The version number of Message Queue for RabbitMQ V2 API is fixed as `2022-01-01`.


Taking enabling public network access (CreatePublicAddress) as an example, the unencoded HTTPS request URL is as follows.

```HTML
https://rabbitmq.byteplusapi.com/?Action=CreatePublicAddress&Version=2022-01-01
```


<span id=".6K-35rGC5pa55rOV"></span>
## Request method

The request method is used to communicate the type of action being performed in the current request to the server. The Message Queue for RabbitMQ currently supports the POST method.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Open API requests include two types of parameters: common request parameters and interface\-specific request parameters. Among them, common request parameters must be included in every interface. For details, see [Common parameters](https://docs.byteplus.com/en/docs/rabbitmq/Common_parameters). Interface\-specific request parameters are unique to each interface. See each interface description for details.

<span id=".6K-35rGC5aS0"></span>
## Request header

The HTTP request header must specify `Content-Type` and authentication parameters. Content\-type defines the structured format of the request body. The Content\-Type for Message Queue for RabbitMQ is fixed as `application/json`. For a detailed list and description of parameters, refer to [Public parameters](https://docs.byteplus.com/en/docs/rabbitmq/Common_parameters).

<span id=".6K-35rGC5raI5oGv5L2T"></span>
## Request message body

The request message body mainly carries other business\-related request parameters. If the request message body parameters support Chinese, the Chinese characters must be UTF\-8 encoded.

The content of the request message body varies for each interface, and not every interface requires one (i.e., the body may be empty). When calling an interface, refer to the API documentation to construct the request body.

<span id=".5Y-R6LW36K-35rGC"></span>
## Make a request

You can send API requests using [curl](https://curl.haxx.se/), [Postman](https://www.getpostman.com/), or by writing code directly. For example, the request example for the CreateInstancePublicAccess interface is as follows.

```JSON
POST https://rabbitmq.byteplusapi.com/?Action=CreatePublicAddress&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceId": "rbtmq-9283a61f****",
   "EipId": "eip-36sveyn9wy39c383g0wbs****"
}
```
