---
title: "Request structure"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Request-structure-v1"
---

This article describes the structure of the message queue Kafka API request.

<span id="e4209537"></span>
## Request URL

You can invoke Kafka's API service by sending an HTTPS POST request. The format of the HTTPS request URL is as follows:

```Plain Text
POST {URI-scheme}://{Endpoint}/?Action={Action}&Version={Version} HTTP/1.1
```


Of which:


* URI\-scheme: Represents the protocol used to transmit requests. All APIs currently use the HTTPS protocol.

* Endpoint: Specifies the server domain name or IP that hosts the service endpoint, i.e. the service address. The endpoint of the message queue Kafka version is `open.ap-southeast-1.byteplusapi.com`.

* Action: The action to be performed, please fill in the API interface to be called here. For the API interface of the message queue Kafka version, please refer to [API overview](https://docs.byteplus.com/en/docs/kafka/API-overview-v1).

* Version: API version number, format is `YYYY-MM-DD` Format. The API version of the message queue Kafka version is `2018-01-01`.


To create a Kafka key as an example, the unencoded HTTPS request URL is as follows.

```plaintext
https://open.ap-southeast-1.byteplusapi.com/?Action=ModifyTopic&Version=2018-01-01
```


<span id="91e4437c"></span>
## Request method

The request method is used to pass the operation type of the current request to the server, and the message queue Kafka version currently supports the POST method.

<span id="3774af6e"></span>
## Request parameters

Byteplus Engine's OpenAPI request contains two types of parameters, namely public request parameters and interface request parameters. Among them, the public request parameters need to be included in each interface, see the detailed description [Common parameters](https://docs.byteplus.com/en/docs/kafka/Common-parameters) Interface request parameters are unique to each interface, see the description of each interface for details

<span id="55fbda4a"></span>
## Request header

You need to specify in the request header of the HTTP request. `Content-Type` And request authentication information and other parameters. Content\-type specifies the structured format of the request message body, and the Content\-Type of the message queue Kafka version is fixed as `application/json`For detailed parameter list and description, please refer to [Common parameters](https://docs.byteplus.com/en/docs/kafka/Common-parameters).

<span id="fb2227f5"></span>
## Request message body

The request message body mainly passes other request parameters related to the business. If the parameters in the request message body support Chinese, the Chinese characters must be UTF\-8 encoded.

The content of the request message body of each interface is different, and not every interface needs to have a request message body (that is, the message body is empty). When calling the interface, please refer to each API interface document to build the request message body.

<span id="c9250179"></span>
## Initiate a request

You can use [Curl](https://curl.haxx.se/),[Mail carrier](https://www.getpostman.com/) or directly write code to send requests and call the API. For example, an example of a request for the ModifyTopic interface is as follows.

```JSON
POST /?Action=ModifyTopic&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****",
  "TopicName": "my_topic",
  "PartitionNumber": 12,
  "MinInsyncReplicaNumber": 2,
  "RetentionHour": 144,
  "MaxMessageMegabyte": 1,
  "Description": "new-describe"
}
```
