---
title: "Request method"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Request-structure"
---

When you call the platform's OpenAPI, it is accomplished by sending requests to a specified service endpoint while fulfilling the platform's signature requirements and the business\-specific parameters of the target API. The request structure of the platform's OpenAPI is organized as follows. Here is an example of an unencoded URL request for DescribeCens:

```Plain Text
GET /?Action=DescribeCens&Version=2020-04-01&<request parameters> HTTP/1.1
Host: cen.byteplusapi.com 
Region: cn-beijing
Service: cen
```

* `GET` indicates that OpenAPI in Cloud Enterprise Network (CEN) only supports Get requests.

* `Action=DescribeCens` specifies the API to call, and `Version=2020-04-01` specifies the API version.

* `Host` specifies the platform's service access address (Endpoint).

* `Region` and `Service` indicate the region and name of the service. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/cen/Public-parameters).

* `HTTP` specifies the communication protocol for the request.

## Service endpoint

The general service endpoints for platform OpenAPI are:  cen.byteplusapi.com

## Communication protocols

Requests can be communicated via either `HTTP` or `HTTPS`. It is recommended to use `HTTPS` for higher security when sending API requests.

## Request method

See the specific requirements of each API for request methods. The CEN OpenAPI supports only GET requests.

> **tip**

* > When using the GET method, the common parameters `Action` and `Version` must be included in the `Query String`.

* > For GET requests, all parameters must be URL\-encoded.

## Request parameters

The platform's OpenAPI requests consist of two types of parameters: Common request parameters and API\-specific request parameters. Common request parameters, included in every API call. For details, see [Common parameters](https://docs.byteplus.com/en/docs/cen/Public-parameters). API request parameters are unique to each API. See the specific API descriptions for details.

## Character encoding

Requests and responses use UTF\-8 character encoding.
