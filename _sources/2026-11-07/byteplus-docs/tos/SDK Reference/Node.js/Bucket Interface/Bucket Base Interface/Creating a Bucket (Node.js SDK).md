---
title: "Creating a Bucket (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-a-bucket-node-js-sdk"
---

A bucket is a globally unique namespace for TOS, which is equivalent to a data container for storing object data. The newly created bucket name must be unique within TOS. This article describes how to create a bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* bucket [Naming Convention](https://docs.byteplus.com/en/docs/tos/docs-common-concepts) As follows:

   * Only lowercase letters a to z, numbers, and dashes (\-) can be included.

   * The beginning and end can only be numbers or letters.

   * The length must be between 3 and 63 characters.

* When accessing TOS through other BytePlus products in the same region as TOS, it is recommended that you use the intranet endpoint. For more information on regions and endpoints, see [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before creating a bucket, you need to ensure that your account has `tos: CreateBucket`permission. You can grant appropriate permissions through IAM policies. For specific steps, see [Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5Yib5bu65a2Y5YKo5qG25pe25bm25Yib5bu65pe25oyH5a6aYWNs"></span>
### When creating a bucket and specifying an ACL when creating

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

const bucketName = 'node-sdk-test-bucket-acl';

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

async function createBucketWithAcl() {
  try {
    // Create a bucket.
    await client.createBucket({
      bucket: bucketName,
      // Specify the storage permission type as private.
      acl: 'private',
    });
    // List all buckets, and list the bucket that was just created.
    const { data } = await client.listBuckets();

    // `theBucket` is the bucket that was just created.
    const theBucket = data.Buckets.find(it => it.Name === bucketName);
    console.log('the bucket info', theBucket);
  } catch (error) {
    handleError(error);
  }
}

createBucketWithAcl();
```


<span id=".5Yib5bu65pe25oyH5a6a5a2Y5YKo57G75Z6L"></span>
### Specify the storage type at creation time

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

const bucketName = 'node-sdk-test-bucket-class';
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
async function createBucketWithStorageClass() {
  try {
    // Create a bucket.
    await client.createBucket({
      bucket: bucketName,
      // Specify the storage class of the bucket as infrequent access storage.
      storageClass: 'IA',
    });
    // List all buckets, and list the bucket that was just created.
    const { data } = await client.listBuckets();

    // `theBucket` is the bucket that was just created.
    const theBucket = data.Buckets.find(it => it.Name === bucketName);
    console.log('the bucket info', theBucket);
  } catch (error) {
    handleError(error);
  }
}

createBucketWithStorageClass();
```


<span id="12b332f5"></span>
### **Specify AZ type when creating**

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError, AzRedundancyType } from '@volcengine/tos-sdk';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'], 
  accessKeySecret: process.env['TOS_SECRET_KEY'], 
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
});

const bucketName = 'node-sdk-test-bucket-az-redundancy';
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
async function createBucketWithAzRedundancy() {
  try {
    // Create a bucket.
    await client.createBucket({
      bucket: bucketName,
      // Specify the storage bucket for multi-AZ.
      azRedundancy: AzRedundancyType.AzRedundancyMultiAz,
    });
    // List all buckets, and list the bucket that was just created.
    const { data } = await client.listBuckets();

    // `theBucket` is the bucket that was just created.
    const theBucket = data.Buckets.find((it) => it.Name === bucketName);
    console.log('the bucket info', theBucket);
  } catch (error) {
    handleError(error);
  }
}

createBucketWithAzRedundancy();
```
