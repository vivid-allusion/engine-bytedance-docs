---
title: "Multipart Upload (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-upload-node-js-sdk"
---

When uploading a large object, it can be divided into multiple data blocks (parts) to upload separately, and finally call merge sharding to merge the uploaded data blocks into one object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before uploading a shard, you must have `tos: PutObject`permission. For details,see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* Before canceling the shard upload task, you must have `tos: AbortMultipartUpload`permission, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* Sharding numbers start from 1 and go up to 10000. Except for the last sharding, all other shardings have a minimum size of 4MiB.

* When uploading an object, the object name must meet certain specifications. For details, see [Common Concepts](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for mass storage. The internal partition stores object index data. In order to scale out the maximum throughput when uploading and downloading objects, and reduce the probability of hot partitions, please avoid using lexicographically increasing object naming.

* If an object with the same name already exists in the bucket, the new object will overwrite the existing object. If versioning is enabled in your bucket, the original object is preserved and a new version number is generated to identify the newly uploaded object.


<span id=".5YiG54mH5LiK5Lyg5q2l6aqk"></span>
## Shard upload steps

Shard uploading generally involves the following three steps:


1. Initialize the shard upload task: Call the createMultipartUpload method to return the globally unique UploadID created by TOS.

2. Upload sharding

   Call the uploadPart method to upload the sharding data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the same shard upload task (identified by the UploadID), the sharding number (PartNumber) identifies the relative position of the sharding in the entire object. If you upload data multiple times through the same sharding number, the original data source will be overwritten in TOS, and the last uploaded data shall prevail.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The response header contains the MD5 value of the data, which can be obtained by Etag. When merging shardings, you need to specify all the sharding information (sharding number, ETag value) in the current shard upload task.   </div>
   

3. Finish sharding upload: When all sharding uploads are complete, call completeMultipartUpload method to merge all shardings into one complete object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5YiG54mH5LiK5Lyg5a6M5pW06L-H56iL"></span>
### **Shard upload complete process**

The following code shows the complete process of uploading local files by sharding, specifying ACL as Private, storage type as low\-frequency storage, and adding custom metadata when uploading.

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { ACLType, StorageClassType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
import fs from 'fs';
import fsp from 'fs/promises';

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
    const bucketName = 'node-sdk-test-bucket';
    const objectName = 'example_dir/multipartExample';
    // The multipartExample file in the local example_dir folder.
    const filePath = './example_dir/multipartExample';
    // Initialize the shard, specify object permissions as private, storage class as infrequent access, and set metadata information.
    const {
      // Get upload task ID
      data: { UploadId },
    } = await client.createMultipartUpload({
      bucket: bucketName,
      key: objectName,
      acl: ACLType.ACLPrivate,
      storageClass: StorageClassType.StorageClassIa,
      meta: { key: 'value ' },
    });
    console.log('CreateMultipartUploadV2 Upload ID:', UploadId);

    // Get local file information and prepare for fragmentation
    const stats = await fsp.stat(filePath);
    // Total file size
    const totalSize = stats.size;
    // Set part size to 5M
    const partSize = 5 * 1024 * 1024;
    let offset = 0;
    // partNumber starts from 1
    let partNumber = 1;
    const partsInfo = [];
    while (offset < totalSize) {
      const uploadResult = await client.uploadPart({
        bucket: bucketName,
        key: objectName,
        partNumber,
        uploadId: UploadId,
        body: fs.createReadStream(filePath, {
          start: offset,
          end: offset + partSize - 1,
        }),
      });
      const eTag = uploadResult.data.ETag;
      console.log(`partNumber${partNumber} Etag:`, eTag);
      partsInfo.push({
        partNumber,
        eTag,
      });
      partNumber++;
      offset += partSize;
    }
    console.log('parts information', partsInfo);

    // Complete chunked upload
    const { data } = await client.completeMultipartUpload({
      bucket: bucketName,
      key: objectName,
      uploadId: UploadId,
      parts: partsInfo,
    });

    console.log('result data:', data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5YiX5Li-5bey5LiK5Lyg5YiG54mH"></span>
### **List uploaded shardings**

The following code enumerates the uploaded sharding information for the specified object in the specified bucket.

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
    const bucketName = 'node-sdk-test-bucket';
    const objectName = '*** Provide your object name ***';
    // Multipart upload task ID can be obtained from the createMultipartUpload interface.
    const uploadId = '*** Provide upload ID ***';

    // List the uploaded shard information for uploadID.
    for (let truncated = true, marker = 0; truncated; ) {
      const { data } = await client.listParts({
        bucket: bucketName,
        key: objectName,
        uploadId,
        partNumberMarker: marker,
      });

      truncated = data.IsTruncated;
      marker = data.NextPartNumberMarker;

      for (const part of data.Parts) {
        console.log(`Part Number: `, part.PartNumber);
        console.log(`ETag: `, part.ETag);
        console.log(`Size: `, part.Size);
      }
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Y-W5raI5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### Cancel shard upload task

You can cancel the shard upload task through **abortMultipartUpload** methods. When a sharding task is cancelled, TOS will delete the uploaded sharding data, and you can no longer perform any operations on the sharding task.

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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    const objectName = '*** Provide your object name ***';
    // Multipart upload task ID, which can be obtained from the createMultipartUpload interface.
    const uploadId = `*** Provide upload ID ***`;

    // Cancel chunked upload task.
    const { data } = await client.abortMultipartUpload({
      bucket: bucketName,
      key: objectName,
      uploadId,
    });

    console.log('result data:', data);
  } catch (error) {
    handleError(error);
  }
}

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

main();
```


<span id="9e85cf25"></span>
## **Related documentation**


* For API documentation on creating a shard upload task, see [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on uploading sharding, see [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart).

* For API documentation on merge sharding, see [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).

* For API documentation on canceling shard upload tasks, see [AbortMultipartUpload](https://docs.byteplus.com/docs/tos/reference-abortmultipartupload).
