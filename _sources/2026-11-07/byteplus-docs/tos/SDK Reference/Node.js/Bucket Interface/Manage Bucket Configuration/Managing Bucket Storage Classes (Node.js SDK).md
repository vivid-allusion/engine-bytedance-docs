---
title: "Managing Bucket Storage Classes (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-storage-types-node-js-sdk"
---

Bucket is the globally unique namespace of TOS, which is equivalent to a data container and is used to store object data. This article describes how to set the storage type of a bucket.

<span id=".5a2Y5YKo57G75Z6L6K-05piO"></span>
## Storage Type Description

Bucket is the globally unique namespace of TOS, which is equivalent to a data container and is used to store object data. TOS provides a variety of bucket storage types, which can be applied to various application scenarios. For more information on storage types, please refer to [Storage Type](https://docs.byteplus.com/docs/tos/docs-storage-type) .This article describes how to set the storage type of a bucket. Bucket storage types include the following categories:


|storage type |describe |Corresponding enumeration value |
|---|---|---|
|Standard storage |Highly available, highly reliable, and high\-performance storage types for frequently accessed data |StorageClassType.*StorageClassStandard* |
|Low Frequency Storage |For data that is accessed infrequently, store it for a minimum of 30 days. |StorageClassType.*StorageClassIa* |
|archive flashback storage |Business scenarios that require long\-term storage and are less accessible, such as archives, should be stored for a minimum of 90 days. |StorageClassType.*StorageClassArchiveFr* |
|Intelligent Tiered Storage |It is suitable for data with uncertain access frequency, and the access layer can be switched according to the access frequency to reduce storage costs. |StorageClassType.*StorageClassIntelligentTiering* |
|cold archive storage |It is a cold data type and is suitable for business scenarios that require minimal access and long\-term storage of data. A minimum of 180 days of storage is required; data needs to be restored before accessing cold archived data. |StorageClassType.*StorageClassColdArchive* |


<span id=".6K6-572u5a2Y5YKo57G75Z6L"></span>
## **Set storage type**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">By default, only the bucket owner has permission to set the bucket storage type.</div>


* <div data-tips="true" data-tips-type="warning">After setting the bucket storage type, if the object storage type is not specified when uploading objects, copying objects, and initializing the shard upload task, the object inherits the bucket storage type.</div>


* <div data-tips="true" data-tips-type="warning">When creating a bucket, if the bucket storage type is not specified, the default storage type is standard storage.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the storage type of the bucket.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError, StorageClassType } from '@volcengine/tos-sdk';

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
    const { requestId: putStorageClassRequestId } = await client.putBucketStorageClass({
      bucket: bucketName,
      storageClass: StorageClassType.StorageClassIa,
    });
    console.log('putBucketStorageClass Request ID: ', putStorageClassRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6I635Y-W6buY6K6k5a2Y5YKo57G75Z6L"></span>
## **Get storage type**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">By default, only the bucket owner has permission to obtain the bucket storage type.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the storage type of the bucket.

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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    const { data, requestId: headBucketRequestId } = await client.headBucket(bucketName);
    console.log('headBucket Request ID: ', headBucketRequestId);
    console.log('Bucket Storage Class: ', data['x-tos-storage-class']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information on storage types, see [Storage Type](https://docs.byteplus.com/docs/tos/docs-storage-type) .
