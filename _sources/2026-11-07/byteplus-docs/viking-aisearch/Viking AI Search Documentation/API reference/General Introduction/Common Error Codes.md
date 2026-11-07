---
title: "Common Error Codes"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Common_Error_Codes"
---

***Viking AI Search*** * is an enterprise\-grade AI search product powered by generative AI. It combines the multimodal semantic representation and understanding capabilities of large models with ByteDance's years of best practices in information retrieval. This provides customers with an out\-of\-the\-box platform to easily build and integrate end\-to\-end multimodal search (for images and text) and recommendation capabilities. To experience more of what Viking AI Search has to offer, visit: * [Viking AI Search Engine, an integrated intelligent engine for enterprise search, recommendation, and Q&A](https://www.volcengine.com/product/AI-Search-Rec)


---



This document lists the common error codes for the AI Search API. This includes APIs for data import/online search, suggestions, and conversational search.

<span id="99b9ee92"></span>
# API Common Error Codes


|**Status Code** |**Error Code** |**Error Message** |**Meaning** |
|---|---|---|---|
|400 |MissingParameter |The request is missing the following parameter: %s |A required parameter is missing. |
|400 |InvalidParameter |A parameter in the request is not valid: {parameters} |**A parameter is invalid. ** This may be due to an incorrect data type, an invalid length, an invalid enum value, or a failure to match the regex pattern. |
|400 |InvalidRequestFormat |The request cannot be parsed in JSON format. |**Failed to parse the request body. ** <br><br>This is typically caused by an invalid request body format, an illegal JSON format, or a structure that does not match the request definition. <br><br>Refer to the corresponding API documentation to check the request structure. |
|400 |InvalidAction |The specified action is invalid: {Action} |The action specified in the request path does not exist or is temporarily unavailable: <br><br><br>*  `write`: Failed to write data, possibly because the dataset resource is not yet created. <br><br>*  `delete`: Failed to delete data, possibly because the dataset resource is not yet created. <br><br>*  `query_completion`: Failed to perform query completion. This may occur if search completion is not configured, the configuration has not taken effect, or no data has been written to the completion index. <br><br>*  `search`: Failed to perform search. This may be because search data is not configured, the search configuration has not taken effect, or no search data has been written. <br><br>*  `browse_index`: Failed to browse the dataset index. This may be because the index has not taken effect after the dataset was associated. <br><br>*  `chat_search`: Failed to perform chat search.<br><br>* `recommend`: Failed to complete recommendation. |
|401 |SignatureNotMatch |The request signature provided is incorrect:{parameters} |**Access Key signature verification failed. ** <br><br>Refer to [API Authentication](https://docs.byteplus.com/docs/viking-aisearch/API_Authentication) checking the authentication signature generation logic, and the validity and correctness of the Access Key and Secret Key. |
|401 |ApiKeyNotValid |The request apikey provided is incorrect:{reason} |**Invalid API key.** <br><br>Go to the [API Key Management](https://console.volcengine.com/aisearch/platform/home/api-key) page to confirm that the API key exists and is active. |
|403 |AccessDenied |The access is denied: {resource} |**Access denied. ** <br><br>The user does not have permission to access this resource. |
|429 |QuotaExceeded |The specified quota has been exceeded: {resource} |**Resource has reached its quota limit. ** <br><br>Create/write operations are not allowed. |
|500 |InternalServiceError |Service has some internal Error. Please Contact with Admin. |An unexpected system error occurred. Try again later or reach out to support.  |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To experience more Viking AI search capabilities, visit the <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search Engine, an all\-in\-one intelligent engine for enterprise search, recommendations, and Q&A</a>.</div>


&nbsp;
