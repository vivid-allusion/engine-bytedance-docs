---
title: "Exception Handling (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Exception-handling-harmony-sdk"
---

This article presents exception handling when using the TOS SDK.

<span id="c7422c47"></span>
## TOS Server\-Side Error

The TOS server complies with HTTP standards and has defined detailed HTTP status codes and business error codes for scenarios involving request failures. For detailed information, please refer to [TOS Server-side Status Codes and Error Codes Definition](https://docs.byteplus.com/en/docs/tos/reference-codes-in-response).

<span id="d2d8bcce"></span>
## SDK Custom Error

<span id="ad3c7a71"></span>
### Client Error \- TosClientError

TosClientError is caused by incorrect client input parameters, connection timeouts, or specific client operations such as canceling a resumable upload. For example, when using createBucket to create a bucket, an exception is raised if the bucket name exceeds 63 characters in length.

<span id="ba602c17"></span>
### Server\-Side Error – TosServerError

Requests are sent to the TOS server via the TOS SDK interface. The response includes status codes that comply with HTTP standards and business error codes, which are used to indicate the response status of the current request.

<span id="afd88350"></span>
### Error Handling Examples

The following code demonstrates exception handling when attempting to download a non\-existent object.

```TypeScript
import { TosClient } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
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
  const bucketName = 'harmony-sdk-test-bucket';
  const objectName = 'object-not-exist'; 

  try {
    await client.getObject({
      Bucket: bucketName,
      Key: objectName,
    });
  } catch (error) {
    handleError(error);
  }
}

main();
```
