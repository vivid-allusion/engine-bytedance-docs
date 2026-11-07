---
title: "Searchinfinity Fetch API Reference"
product: "Searchinfinity"
product_code: "searchinfinity"
source: "https://docs.byteplus.com/en/docs/searchinfinity/Searchinfinity_Fetch"
---

This document describes the input and output parameters of the Searchinfinity Fetch API. You can call this API to fetch content from a specified URL and adapt the returned data for your project.

<span id="iDix7Psj"></span>
# Authentication

This API supports access by API key.

<span id="xzMI425J"></span>
## Obtain an API key 


* Open and log in to [SearchInfinity API Key Management](https://console.byteplus.com/search-infinity/api-key).

* Click **Create API Key** to go to the creation page.

* Enter an API key name and create the key.


> Note: Store your API key securely. We strongly recommend that you do not hard\-code it in your application code or commit it to a public repository.


<span id="LegbURtI"></span>
## Construct the signature

API key signature authentication requires you to add the Authorization field to the HTTP request header as follows:

```JSON
Authorization: Bearer <API_KEY>
```


> **Note:**  When using API key access, the default API timeout is 60 seconds.


<span id="LTJkaoHL"></span>
# API Details

<span id="jeVFUJtT"></span>
## URL


|**Field** | |
|---|---|
|URL |https://torchlight.byteintlapi.com/search_api/fetch |
|Method |POST |
|Content\-Type |application/json |


<span id="qUZqvrwR"></span>
## Request


|**Field** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Url |String |Yes |The URL of the page to fetch. Only URLs starting with `http://` or `https://` are supported.Pass a single URL as a string, for example `https://www.example.com/article`[.](https://www.example.com/article.) A URL array is not supported. |


<span id="y9ZQZBzv"></span>
## Response


|**Field** |**Type** |**Required** |**Description** |
|---|---|---|---|
|ResponseMetadata |Object |Yes |Unified response metadata. |
|Result |FetchResponse |No |Returned when the request succeeds; `null` when the API\-layer call fails. The access status of the target page is indicated by `Data.StatusCode`. |


<span id="tDr23Kdy"></span>
### ResponseMetadata


|Field |Type |Required |Description |
|---|---|---|---|
|RequestId |String |Yes |The request ID, aligned with `X-Tt-Logid` in the response header. |
|Action |String |Yes |An empty string for this API path. |
|Version |String |Yes |An empty string for this API path. |
|Service |String |Yes |An empty string for this API path. |
|Region |String |Yes |An empty string for this API path. |
|Error |Object |No |API\-layer error information. This field is populated for errors such as RPC failures, parameter errors, authentication failures, and unavailable plans. |


<span id="D4Jy77xy"></span>
### FetchResponse


|Field |Type |Required |Description |
|---|---|---|---|
|Data |FetchData |Yes |The main body of the fetch result. For details, see FetchData. |
|LogId |String |Yes |The log ID. It is the same as `X-Tt-Logid` in the response header. |
|TimeCost |Number |Yes |The time cost, in milliseconds. |


<span id="j9fQOdi8"></span>
### FetchData


|**Field** |**Type** |**Required** |**Description** |
|---|---|---|---|
|StatusCode |Number |Yes |The HTTP status code returned by the target page, for example 200 (success) or 404 (page not found). The error status returned by the target site is expressed through this field and is handled separately from the API\-layer error in `ResponseMetadata.Error`. |
|Url |String |Yes |The original request URL. |
|RedirectedUrl |String |No |The final URL after redirection. This field is empty if the target page is not redirected. |
|Title |String |No |The page title. This field is empty if the title cannot be parsed. |
|PublishTime |Number |No |The page publication time, as a Unix timestamp in seconds. This field is empty if the publication time cannot be parsed. |
|ContentText |String |No |The body text content of the page. Up to 50,000 characters are returned. This field is empty if no body text is parsed. A successful page visit does not guarantee that body text can be parsed. |


> Note: The types in the table apply when a field has a value. In the examples below, `null` indicates optional information that was not retrieved. When integrating, handle missing fields or `null` values, and check whether `ContentText` is an empty string before using it.


<span id="c14Yz25N"></span>
## **Request Example**

```JSON
{
  "Url": "https://example.com/article"
}
```


<span id="AGP0tSDb"></span>
## **Response Example**

The following examples illustrate the response structure. Actual field values are subject to the real response.

<span id="UY5pMZTX"></span>
### Successful Request Example

The target page is visited successfully, and the parsed title, publish time, and body text are returned.

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2026070814000000000000000000000000",
    "Action": "Fetch",
    "Version": "2025-01-01",
    "Service": "volc_torchlight_api",
    "Region": "cn-beijing"
  },
  "Result": {
    "Data": {
      "StatusCode": 200,
      "Url": "https://example.com/article",
      "RedirectedUrl": "https://www.example.com/article",
      "Title": "Example Article",
      "PublishTime": 1783308483,
      "ContentText": "This is the main content extracted from the target page."
    },
    "LogId": "2026070814000000000000000000000000"
    "TimeCost": 7854
  }
}
```


<span id="7I83XNzL"></span>
### Target Page Access Error Example

The API call completes normally, but the target page returns 404 (page not found). This status is returned through `Result.Data.StatusCode` and is not an API\-layer error indicated by `ResponseMetadata.Error`. In this example, the title, publish time, and body text are not parsed, so those fields are `null`.

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026091400000000000000000000000001",
        "Action": "",
        "Version": "",
        "Service": "",
        "Region": ""
    },
    "Result": {
        "Data": {
            "StatusCode": 404,
            "Url": "https://www.example.com/not-found",
            "RedirectedUrl": null,
            "Title": null,
            "PublishTime": null,
            "ContentText": null
        },
        "LogId": "2026091400000000000000000000000001",
        "TimeCost": 1532
    }
}
```


<span id="WbiqzQWv"></span>
### Error Response Example

The API call completes normally, but the target page returns 404 (page not found). This status is returned through Result.Data.StatusCode and is not an API\-layer error indicated by ResponseMetadata.Error. In this example, the title, publish time, and body text are not parsed, so those fields are null.

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2026070814000000000000000000000002",
    "Action": "Fetch",
    "Version": "2025-01-01",
    "Service": "volc_torchlight_api",
    "Region": "cn-beijing",
    "Error": {
        "CodeN": 700901,
        "Code": "invalid_api_key",
        "Message": "invalid api key"
    }
  },
  "Result": null
}
```


<span id="JUjDjood"></span>
# Usage notes


* **Static content only.**  This API parses only the static content of a page and does not execute JavaScript. Content that relies on JavaScript to load dynamically may not be retrieved.

* **Single URL per request.**  Each request accepts one complete HTTP or HTTPS URL. A URL array is not supported.

* **Body text length.**  `ContentText` returns up to 50,000 characters. When the title, publish time, or body text cannot be parsed, the corresponding field is empty. A successful page visit does not guarantee that body text can be parsed.

* **robots and access compliance.**  Page fetching is subject to the target site's robots policy and access\-compliance checks. When a URL does not pass these checks, the fetch is rejected. Change the URL, and do not repeat the request for the same URL.

* **Fetch timeout and success rate.**  The default API **timeout is 60 seconds**. The fetch **may fail if the fetch link times out, the protocol is abnormal, or the page content cannot be parsed**; you can retry later. Because the outcome depends on the target site, a successful fetch is not guaranteed for every URL.

* **Request rate.**  The request rate limit is subject to the value shown in the console. If you exceed the limit, reduce your request frequency and retry.

* **Compliant use.**  Follow the target site's terms of service and access rules, and make sure you have a lawful basis for access and automated retrieval. Do not bypass login, paywalls, CAPTCHAs, or other access controls. Your use of the service must also comply with the applicable BytePlus terms.


<span id="Py6hYY6Y"></span>
# Error Handling


|**Error Code** |**Description** |**Recommended Check or Action** |
|---|---|---|
|10400 |General parameter error |Check the request structure. This is usually caused by an incorrect field type. |
|10403 |Permission error |Check whether the account has enabled the corresponding service. |
|10500 |Default internal error |A fallback server\-side error code. In most cases, retrying the request can resolve the issue. |
|700901 |Invalid API key |Check whether the API key is provided and whether it is provided correctly. See “Authentication”. |
|700429 |QPS limit exceeded |Control the number of concurrent search requests per second. The default QPS is 5. |
|10403 |Free quota exhausted |Check in the online search console whether paid API calls have been enabled. |


<span id="FcVZOzco"></span>
# Changelog


|**Version** |**Update** |**Update Date** |
|---|---|---|
|V1.0.0 |Added the Fetch API documentation, covering the request, response, examples, and error handling. |2026.07.08 |
|V1.0.1 |Supplemented ResponseMetadata; updated the TimeCost field in FetchResponse, the request example, and the successful response example; removed the description and specific QPS value for error code 700429. |2026.09.22 |


<span id="yY7QjSYw"></span>
#
