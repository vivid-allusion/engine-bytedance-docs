---
title: "Retrieve iOS SDK responses (legacy)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/getting_ios_sdk_response_information"
---

The TLS iOS SDK provides a unified response wrapper for each implemented interface. This document describes how to obtain various response information from the SDK.

## Retrieve request response fields

You can use `response.fieldName` to obtain the return fields of each API described in  [CreateProject](https://docs.byteplus.com/docs/tls/api-createproject). Code example:

```objectivec
......
DescribeProjectsResponse *response = [client DescribeProjects:request];
NSLog(@"HttpStatusCode: %@", response.fieldName);
......
```

## Retrieve the HTTP status code

You can use `response.statusCode` to obtain the response code for the request. Code example:

```objectivec
......
DescribeProjectsResponse *response = [client DescribeProjects:request];
NSLog(@"HttpStatusCode: %@", response.statusCode);
......
```

## Retrieve error information

If the response code is not 200, you can use `response.errorCode` and `response.errorMessage` to obtain the error code and error description, which can help you troubleshoot issues. Code example:

```objectivec
......
DescribeProjectsResponse *response = [client DescribeProjects:request];
NSLog(@"ErrorCode: %@, ErrorMessage: %@", response.errorCode, response.errorMessage);
......
```

## Retrieve the request RequestId

To obtain assistance from TLS support when encountering difficulties during TLS API calls, you can use `response.requestId` to record the `requestId` of the Exception request and provide it to TLS staff for faster issue response and resolution. Code example:

```objectivec
......
DescribeProjectsResponse *response = [client DescribeProjects:request];
NSLog(@"RequestId: %@", response.requestId);
......
```

## Serialize the request response as a JSON string

You can also directly serialize the response using the `toJSONString` method to visually inspect the request response. Code example:

```objectivec
......
DescribeProjectsResponse *response = [client DescribeProjects:request];
NSLog(@"Response json string: %@", [response toJSONString]);
......
```
