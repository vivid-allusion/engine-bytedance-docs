---
title: "Exception Handling (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Exception-handling-node-js-sdk"
---

This document describes exception handling when using the TOS SDK.

<span id=".dG9zLeacjeWKoeerr-mUmeivrw=="></span>
## TOS Server\-Side Error

The TOS server adheres to HTTP specifications and defines detailed HTTP status codes and business error codes for scenarios involving request failures. For detailed information, please refer to [TOS Server-Side Status Codes and Error Codes Definition](https://docs.byteplus.com/en/docs/tos/reference-codes-in-response).

<span id=".c2RrLeiHquWumuS5iemUmeivrw=="></span>
## SDK Custom Errors

<span id=".5a6i5oi356uv6ZSZ6K-vLXRvc2NsaWVudGVycm9y"></span>
### Client Error – TosClientError

TosClientError is caused by incorrect client input parameters, connection timeouts, or the execution of special operations by the client, such as canceling a breakpoint resume upload. For example, when using createBucket to create a bucket, an exception is raised if the bucket name exceeds 63 characters in length.

<span id=".5pyN5Yqh56uv6ZSZ6K-vLXRvc3NlcnZlcmVycm9y"></span>
### Server\-side Error \- TosServerError

Requests are sent to the TOS server via the TOS SDK interface. The response includes status codes that comply with HTTP standards and business error codes, which indicate the response status of the current request.

<span id=".6ZSZ6K-v5aSE55CG56S65L6L"></span>
### Error Handling Examples

The following code demonstrates exception handling when attempting to download a non\-existent object.

```javascript
import { TosClient } from '@volcengine/tos-sdk';

const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'], 
  accessKeySecret: process.env['TOS_SECRET_KEY'], 
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

function handleError(error) {
  if (error instanceof TosClientError) {
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Header:', error.headers);
    console.log('Response Err Code:', error.code);
    console.log('Response Err Msg:', error.message);
  } else {
    console.log('unexpected exception, message: ', error);
  }
}

async function main() {
  const bucketName = 'node-sdk-test-bucket'; 
  const objectName = 'object-not-exist'; 

  try {
    await client.getObjectV2({
      bucket: bucketName,
      key: objectName,
    });
  } catch (error) {
    handleError(error);
  }
}

main();
```
