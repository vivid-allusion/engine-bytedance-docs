---
title: "Retrieve Bucket Information (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-information-node-js-sdk"
---

Get the information of the bucket through the HeadBucket, and at the same time, you can determine whether the bucket exists according to the HTTP Code information in the returned err. This article describes how to obtain bucket metadata and determine whether a bucket exists.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before you can get the bucket metadata, you must have the `tos: HeadBucket`permission. For specific operations, please refer to [Overview](https://docs.byteplus.com/docs/tos/docs--overview)

* If the bucket does not exist, the interface returns a 404, which is also commonly used to determine whether a bucket exists.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id="8c376b3e"></span>
### **Determine whether the bucket exists**

```JavaScript
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

const bucketName = 'node-sdk-test-bucket-not-exist';
async function main() {
  try {
    // Check if the bucket exists.
    const { data } = await client.headBucket(bucketName);

    console.log(`the region of ${bucketName} is`, data['x-tos-bucket-region']);
    console.log(`the storageClass of ${bucketName} is`, data['x-tos-storage-class']);
  } catch (error) {
    if (error instanceof TosServerError) {
      if (error.statusCode === 404) {
        // The bucket does not exist.
        console.log('Bucket not found.');
        return;
      }
    }

    handleError(error);
  }
}

main();
```


<span id="29233264"></span>
### **Get bucket metadata**

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
   // Get bucket metadata information.
   const { data } = await client.headBucket(bucketName);

   console.log(`the region of ${bucketName} is`, data['x-tos-bucket-region']);
   console.log(`the storageClass of ${bucketName} is`, data['x-tos-storage-class']);
 } catch (error) {
   handleError(error);
 }
}

main();
```
