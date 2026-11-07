---
title: "List Buckets (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-buckets-node-js-sdk"
---

Get a list of buckets through ListBuckets. You can list the storage spaces that meet the specified criteria in all regions of your current account.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before enumerating buckets, you must have `tos: ListBuckets`permission. For specific operations, please refer to [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* The ListBuckets interface returns buckets for all regions of the current account.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code enumerates the buckets in all areas of the current account.

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'], 
  accessKeySecret: process.env['TOS_SECRET_KEY'], 
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
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
  try {
    const { data } = await client.listBuckets();
    console.log(`listBuckets data: `, data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="74dd05de"></span>
## **Related documentation**

For API documentation on enumerating buckets, see [ListBuckets](https://docs.byteplus.com/docs/tos/reference-listbuckets).
