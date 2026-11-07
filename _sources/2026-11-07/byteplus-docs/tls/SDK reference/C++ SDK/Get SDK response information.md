---
title: "Get SDK response information"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_c_response_information"
---

Torch Log Service (TLS) SDK for C++ offers a unified style of encapsulated responses for API actions. This topic describes how to get SDK response information.

<span id="获取请求响应字段"></span>
## Getting the response fields

Use `response.fieldName` to get the response fields of an API action described in [API overview](https://docs.byteplus.com/docs/tls/API-overview). Sample code:

```cpp
...
auto response = client.DescribeProjects(request);
printf("%d\n", response.total);
...
```


<span id="获取-http-状态码"></span>
## Getting the HTTP status code

Use `response.http_status_code` to get the response code. Sample code:

```cpp
...
auto response = client.DescribeProjects(request);
printf("%d\n", response.http_status_code);
...
```


<span id="获取错误信息"></span>
## Getting the error information

If the response code is not 200, use `response.error_code` and `response.error_message` to get the error code and error message returned by the TLS server for troubleshooting. Sample code:

```cpp
...
auto response = client.DescribeProjects(request);
printf("error_code: %s error_message: %s\n", response.error_code.c_str(), response.error_message.c_str());
...
```


<span id="获取请求-requestid"></span>
## Getting the request ID

If you encounter an issue when calling a TLS API action and need help, contact TLS customer service support and provide the exception `requestId` recorded by `response.request_id` for a quick response. Sample code:

```cpp
...
auto response = client.DescribeProjects(request);
printf("request_id: %s\n", response.request_id.c_str());
...
```


<span id="将请求响应序列化为-json-字符串"></span>
## Serializing a response to a JSON string

The response objects of TLS SDK for C++ support using the [GitHub - nlohmann/json: JSON for Modern C++](https://github.com/nlohmann/json) library for serialization and deserialization.

This allows you to directly serialize the response to view the response clearly. Sample code:

```cpp
#include <ve-tls-cpp-sdk/thirdparty/nlohmann/json.hpp>

...
auto response = client.DescribeProjects(request);
nlohmann::json j = response;
printf("response: %s", j.dump().c_str());
...
```
