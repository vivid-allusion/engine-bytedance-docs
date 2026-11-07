---
title: "Retrieving Bucket Information (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-information-harmony-sdk"
---

You can use HeadBucket to retrieve information about a bucket. Additionally, the HTTP Code in the returned error can be used to determine whether the bucket exists. This article describes how to obtain bucket metadata and determine whether a bucket exists.

<span id="24695ed1"></span>
## Precautions


* Before you can retrieve bucket metadata, you must have the `tos:HeadBucket` permission.

* If the bucket does not exist, the interface will return a 404 error code; it is also commonly used to determine whether a bucket exists.


<span id="9d4abc62"></span>
## Sample Code

<span id="b4219301"></span>
### **Determine whether the bucket exists**

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
  region: "Provide your region",  
  endpoint: "Provide your endpoint", 
});

function handleError(error: Error) {
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

const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {
  try {
   
    const res = await client.headBucket({
      Bucket: bucketName
    });

    console.log(`the region of ${bucketName} is`, res.Region);
    console.log(`the storageClass of ${bucketName} is`, res.StorageClass);
  } catch (error) {
    if (error instanceof TosServerError) {
      if (error.StatusCode === 404) {
       
        console.log('Bucket not found.');
        return;
      }
    }

    handleError(error);
  }
}

main();
```


<span id="4406f732"></span>
### **Retrieve Bucket Metadata**

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

function handleError(error: Error) {
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

const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {
  try {
   
    const res = await client.headBucket({
      Bucket: bucketName
    });

    console.log(`the region of ${bucketName} is`, res.Region);
    console.log(`the storageClass of ${bucketName} is`, res.StorageClass);
    console.log(`the azRedundancy of ${bucketName} is`, res.AzRedundancy)
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="dbeda4d9"></span>
## **Related Documents**

For documentation on the API for retrieving bucket metadata, see [HeadBucket](https://docs.byteplus.com/docs/tos/reference-headbucket).
