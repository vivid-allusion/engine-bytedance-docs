---
title: "Request structure"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/request-structure-v2"
---

This article describes the structure of the message queue Kafka API request.

<span id="bdc1bafb"></span>
## Request URL

You can invoke Kafka's API service by sending an HTTPS POST request. The format of the HTTPS request URL is as follows:

```Bash
POST {URI-scheme}://{Endpoint}/?Action={Action}&Version={Version} HTTP/1.1
```


Of which:


* URI\-scheme: Represents the protocol used to transmit requests. All APIs currently use the HTTPS protocol.

* Endpoint: Specifies the server domain name or IP that hosts the service endpoint, that is, the service address. The service address of the message queue Kafka is `open.ap-southeast-1.byteplusapi.com`.

* Action: The action to be performed, please fill in the API interface to be called here. For the API interface of the message queue Kafka version, please refer to [API overview](https://docs.byteplus.com/en/docs/kafka/API-overview-2).

* Version: API version number, format is `YYYY-MM-DD` Format. The API version of the message queue Kafka version is `2022-05-01`.


To create a Kafka key as an example, the unencoded HTTPS request URL is as follows.

```Bash
https://open.ap-southeast-1.byteplusapi.com/?Action=ModifyTopic&Version=2022-05-01
```


<span id="3c71850f"></span>
## Request method

The request method is used to pass the operation type of the current request to the server, and the message queue Kafka version currently supports the POST method.

<span id="0516f632"></span>
## Request parameters

Byteplus Engine's OpenAPI request contains two types of parameters, namely public request parameters and interface request parameters. Among them, the public request parameters need to be included in each interface, see the detailed description [Common parameters](https://docs.byteplus.com/en/docs/kafka/common-parameters-v2) Interface request parameters are unique to each interface, see the description of each interface for details.

<span id="b6e95e43"></span>
## Request header

You need to specify in the request header of the HTTP request. `Content-Type` And request authentication information and other parameters. Content\-type specifies the structured format of the request message body, and the Content\-Type of the message queue Kafka version is fixed as `application/json`For detailed parameter list and description, please refer to [Common parameters](https://docs.byteplus.com/en/docs/kafka/common-parameters-v2) .

<span id="bbf0aa28"></span>
## Request message body

The request message body mainly passes other request parameters related to the business. If the parameters in the request message body support Chinese, the Chinese characters must be UTF\-8 encoded.

The content of the request message body of each interface is different, and not every interface needs to have a request message body (that is, the message body is empty). When calling the interface, please refer to each API interface document to build the request message body.

<span id="c8ff9cd6"></span>
## Initiate a request

You can use [Curl](https://curl.haxx.se/),[Mail carrier](https://www.getpostman.com/) or directly write code to send requests and call the API. For example, an example of a request for the ModifyTopic interface is as follows.

```JSON
POST /?Action=CreatePublicAddress&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka
```
