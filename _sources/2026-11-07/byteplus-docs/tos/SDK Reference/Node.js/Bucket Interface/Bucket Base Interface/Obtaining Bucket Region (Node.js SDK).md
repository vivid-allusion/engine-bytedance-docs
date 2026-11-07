---
title: "Obtaining Bucket Region (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-the-bucket-region-node-js-sdk"
---

A bucket is a globally unique namespace for TOS, which is equivalent to a data container for storing object data. This article describes how to obtain the regional information where the bucket is located.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* By default, only the owner of the bucket can view the region where the bucket is located.

* When using the TOS Node.js SDK to manage buckets and the objects within them, you must use the domain name of the bucket's domain. For more information on regions and access domains, please refer to [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code is used to obtain the region of the bucket.

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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    const { data } = await client.getBucketLocation({ bucket: bucketName });
    // View bucket region.
    console.log('Bucket Region:', data.Region);
    // View the bucket's public endpoint
    console.log('Bucket ExtranetEndpoint:', data.ExtranetEndpoint);
    // View the bucket's internal endpoint
    console.log('Bucket IntranetEndpoint:', data.IntranetEndpoint);
  } catch (error) {
    handleError(error);
  }
}

main();
```
