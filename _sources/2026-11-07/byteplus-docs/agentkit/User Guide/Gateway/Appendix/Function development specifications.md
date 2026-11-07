---
title: "Function development specifications"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Function_development_specifications"
---

When using the custom service extension plugin for a dedicated gateway, you need to develop and deploy the function yourself. The function must comply with the following protocol specifications. Otherwise, the result is considered invalid. Depending on whether "Fail open" is enabled, the gateway either returns a 500 error or skips the plugin and continues processing the request.

## Request structure

When the gateway invokes the function, it sends a request body with the following structure:

```JSON
{
  "request": {
    "headers": <xxx>,   // Request headers
    "body": <xxx>      // Request body, Base64-encoded. It exists only when "Pass body" is enabled.
  },
  "response": {          // This field exists only in requests during the response phase.
    "headers": <xxx>
    "body": <xxx>      // Response body, Base64-encoded. It exists only when "Pass body" is enabled.
  },
  "properties": Record   // Context properties, including requestId, consumerName (maps to user ID in OAuth JWT scenarios), and resourceId (MCP service ID, etc.)
}
```

### Sample value

The following example shows the gateway invoking the function during the request phase. In this example, the request `body` is Base64\-encoded. When decoded, it is `{"query":"hello"}`。

```JSON
{
  "request": {
    "headers": {
      "accept":[
          "application/json",
          "application/x-www-form-urlencoded"
     ], 
     "content-type": "application/json"
    },
    "body": "eyJxdWVyeSI6ImhlbGxv****"
  },
  "properties": {
    "requestId": "550e8400-e29b-41d4-a716-44665544****",
    "consumerName": "6fa459ea-ee8a-3ca4-894e-db77e160****",
    "resourceId": "m-yeujh184xs64rmgq****"
  }
}
```

## Response structure

After processing, the function must return a response body with the following structure:

```JSON
{
  "request": {
    "headers": <xxx>,  // Differential modification of request headers. Valid only during the request phase.
    "body": <xxx>      // Modified request body, Base64-encoded.
  },
  "response": {
    "headers": <xxx>,  // Differential modification of response headers.
    "body": <xxx>      // Modified response body, Base64-encoded.
  }
}
```

### Sample value

The following example shows the function instructing the gateway to modify response headers and replace the response body with new JSON content. In this example, `response.body` is Base64\-encoded. When decoded, it is `{"message":"handled by function"}`。

```JSON
{
  "response": {
    "headers": {
      "x-function-processed": [
        "true"
      ],
      "content-type":"application/json"
    },
    "body": "eyJtZXNzYWdlIjoiaGFuZGxlZCBieSBmdW5jd****"
  }
}
```

If you only need to modify `headers`, return only `response.headers`. If you do not need to modify the `body`, omit `response.body`.

## Response specification

### Validity requirements

* Custom service extension responses must be valid and semantically correct, with correct types.

* The `:method`, `:path`, and `:authority` fields in request headers must comply with HTTP specifications.

* The `:status` field in response headers must be parseable as an integer in the range 200–599.

### Semantics for differential header modification

Headers are modified based on the `request.headers `and `response.headers` fields in the returned result, using patch semantics.

* Headers not provided are left unchanged.

* A header with a **null** value is deleted.

* A header with a non\-**null** value is overwritten.

* Header values must not be empty arrays.

### Body modification constraints

* Both `request.body` and `response.body` are Base64\-encoded.

* The custom service extension in the request phase can modify the request body only when "Pass body" is **enabled ** and the ** request body is not empty**.

* The custom service extension in the response phase can modify the response body only when "Pass body" is **enabled ** and ** the response body is not empty**.

### Early return in the request phase

The function in the request phase can include a `response` field in its invocation response to trigger an early termination and return directly without forwarding to the backend service. In this case:

* `response.headers` must contain complete response headers and must include a valid `:status`.

* `response.body` must exist and must not be empty.

### Ignore `request` during the response phase

If a `request` field is included in a response\-phase response, it is ignored.
