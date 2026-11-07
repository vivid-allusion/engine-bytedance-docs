---
title: "Components of an API request"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/components-of-an-API-request"
---

This topic describes the components of an API request.

AnAPI request can be separated into three components:


* The request URI

* HTTP request message header

* Optional HTTP request message body


Each API document provides a request example for your reference. Please encode it yourself before sending the request. If the interface call is successful, the return parameters will be displayed; if the call fails, the corresponding error message will be displayed, and you can analyze and troubleshoot based on the error code.

<span id="the-request-uri"></span>
## The request URI

The request URI consists of:

```Plain
https://tls-{Region}.bytepluses.com/{Action}?&parameters
&<common request parameters>
```



* `tls-{Region}.bytepluses.com`：Specifies the domain name or IP address of the server where the service endpoint is hosted. For more information, see Endpoint.

* Action：Specifies the the operations.

* parameters：The request parameters of the API in the URL. Query\-type API interfaces need to pass business parameters in the request URL, such as Describe\* and other APIs; other API interfaces directly pass business parameters in the Body.

* Common request parameters：Other required common request parameters.


For example, you might send an HTTPS GET request method by using request header fields that are similar to the following:

```Plain
GET https://tls-cn-beijing.bytepluses.com/DescribeProjects?PageNumber=1&PageSize=10
```


<span id="request-message-header"></span>
## Request message header

In the request header (Header) of the HTTP request, common parameters such as Content\-Type and request authentication information need to be specified to identify the user and interface signature. Unless necessary, these parameters will not be explained in each individual interface document, but these parameters need to be carried in each request in order to normally initiate the request.

Among them, Content\-Type specifies the structured format of the request message body, and the Content\-Type of the log service is fixed as application/json.

<span id="request-message-body"></span>
## Request message body

The request message body mainly transmits business\-related request parameters. If the parameters in the request message body support Chinese characters, the Chinese characters must be encoded in UTF\-8.

The content of the request message body of each interface is different, and not every interface requires a request message body (that is, the message body is empty). When invoking the interface, please refer to the documentation of each API interface to construct the request message body.

<span id="request-method"></span>
## Request method

The request method is used to convey the operation type of the current request to the server. The following are the HTTP request methods supported by the log service.


|Method |Description |
|---|---|
|GET |Requests the server to return the specified resource. |
|PUT |Requests the server to update the specified resource. |
|POST |Requests the server to add new resources or perform special operations. |
|DELETE |Requests the server to delete the specified resource. |


<span id="send-the-request"></span>
## Send the request

You can send requests to invoke the API using methods such as curl, Postman, or directly writing code. For example, here is a request example for the ModifyProject interface.

```json
PUT https://tls-{Region}.bytepluses.com/ModifyProject HTTP/1.1
Content-Type: application/json
...
{
    "ProjectName":"newproject",
    "Description":"server log",
    "ProjectId":"20e84633-51a0-4006-8bfd-f16235d0****"
}
```
