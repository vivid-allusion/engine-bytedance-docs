---
title: "BytePlus Recommend API HTTP request"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-api_http_request"
---

This topic uses `WriteUsers` as an example to introduce how to make API HTTP requests in BytePlus Recommend. A complete HTTP request includes three parts:


* request URL

* request methods

* request parameters


<span id="50dd9a3b"></span>
## Request URL

Request URL:`{URI-scheme}://{Endpoint}/?{query-string}`

For a more detailed description of the URL components, refer to the following table:


|**Component** |**Description** |
|---|---|
|URI\-scheme |Supports HTTP and HTTPS. For security purposes, we recommend HTTPS. For more information on using HTTPS, refer to [Data security](https://docs.byteplus.com/recommend/resources/data_security). |
|Endpoint |The location where the API receives requests. The endpoint of the BytePlus Recommend API is `rec-api-sg1.recplusapi.com`. |
|query\-string |Includes shared request parameters and operation\-specific parameters.<br><br>For operation\-specific parameters and a partial list of shared request parameters, see the detailed description of each API operation.<br><br>For a complete list of shared request parameters, refer to Shared BytePlus Recommend parameters. |


For example, the request URL of `WriteUsers` is as follows:

```JSON
https://rec-api-sg1.recplusapi.com/RetailSaaS/WriteUsers 
```


<span id="d124473d"></span>
## Request methods

Request methods inform the server of the method to be performed on the resource. The BytePlus Recommend API supports the following request methods:


|**Method** |**Description** |
|---|---|
|POST |Creates a resource |


The request method of `WriteUsers` is POST. The full request URL is as follows:

```JSON
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/RetailSaaS/WriteUsers \
```


<span id="381acb23"></span>
## Request parameters

An HTTP request should include information on the following types:


* API request parameters: Refer to the reference topics for specific APIs.


<span id="ee66522b"></span>
## Request example

A complete request for `WriteUsers` is as follows:

```JSON
curl --request POST \
     --url https://rec-api-sg1.recplusapi.com/RetailSaaS/WriteUsers \
     --header 'Tenant-Id: 3000001813' \
     --header 'Request-Id:12313208' \
     --header 'accept: application/json' \
     --header 'content-type: application/json' \
     --data '
{
  "project_id": "851467130",
  "stage": "production",
  "data": [
    "{\"user_id\":\"14577890\",\"gender\":\"male\",\"age\":\"23\",\"tags\":\"[\\\"new user\\\",\\\"low purchasing power\\\",\\\"bargain seeker\\\"]\",\"activation_channel\":\"AppStore\",\"membership_level\":\"silver\",\"registration_timestamp\":1623593487,\"city\":\"Kirkland\",\"country\":\"USA\",\"district\":\"King County\",\"province\":\"Texas\",\"language\":\"English\"}"
  ]
}
'
```
