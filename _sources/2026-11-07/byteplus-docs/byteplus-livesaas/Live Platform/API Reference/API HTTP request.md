---
title: "API HTTP request"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-api-http-request"
---

To call the BytePlus Live API, you must construct a standard HTTP request. This guide explains the fundamental structure of an API HTTP request, including the request URL, methods, and parameters, using the `CreateActivityAPIV2` API as a practical example.

A complete HTTP request includes three parts:


* request URL

* request methods

* request parameters


<span id="request-url"></span>
## Request URL

Request URL: `{URI-scheme}://{Endpoint}/?{query-string}`

The following table describes the URL components.


|**Component** |**Description** |
|---|---|
|URI\-scheme |Supports HTTP and HTTPS. For security purposes, we recommend HTTPS. |
|Endpoint |The service endpoint where the API receives requests. The endpoint of the BytePlus Live API is `livesaas.byteplusapi.com`. |
|query\-string |Includes shared request parameters and operation\-specific parameters.<br><br>For operation\-specific parameters and a partial list of shared request parameters, see the detailed description of each API operation.<br><br>For a complete list of shared request parameters, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967). |


For example, the request URL of `CreateActivityAPIV2` is as follows:

```JSON
http://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
```


<span id="request-methods"></span>
## Request methods

A request method specifies the action to perform on a resource. The BytePlus Live API supports the following request methods:


|**Method** |**Description** |
|---|---|
|GET |Retrieves specified resources. Public data can be sent in the request headers and query string parameters. |
|POST |Sends requests to the server to add resources or perform special operations. Public data can be added to headers only. |


The request method of `CreateActivityAPIV2` is POST. The request line is as follows:

```JSON
POST http://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
```


<span id="request-parameters"></span>
## Request parameters

An HTTP request includes the following types of parameters:


* Shared parameters: For more information, refer to [Shared parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters).

* API request parameters: Refer to the reference topics for specific APIs.


<span id="request-example"></span>
## Request example

A complete request for `CreateActivityAPIV2` is as follows:

```JSON
POST http://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
{
    "Name":"Live Room A",
    "LiveTime":1642668850
}
```
