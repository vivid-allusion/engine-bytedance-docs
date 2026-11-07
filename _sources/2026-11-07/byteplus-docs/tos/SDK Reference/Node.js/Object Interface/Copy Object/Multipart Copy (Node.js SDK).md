---
title: "Multipart Copy (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Sharding-copy-node-js-sdk"
---

When the object is larger than 5GiB, you need to use uploadPartCopy to make a sharding copy.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Copy files do not support inter\-barrel copying across regions.

* When copying an object, the account must have read access to the source object and write access to the destination bucket.

* When copying an object, you can either preserve all metadata (the default) or specify new metadata. However, the ACL is not preserved, but is set to private.


<span id=".5YiG54mH5ou36LSd5q2l6aqk"></span>
## Sharding copy steps


1. Initialize the sharding copy task with createMultipartUpload.

2. Sharding the copy via uploadPartCopy.

3. Merge sharding by completeMultipartUpload.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

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
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
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
    const srcBucket = 'node-sdk-test-bucket'; // Source bucket
    const srcObject = 'source-test'; // Source object
    const dstBucket = 'node-sdk-copy-bucket'; // Target bucket
    const dstObject = 'copy-test'; // Target object

    // Get upload task ID.
    const {
      data: { UploadId },
    } = await client.createMultipartUpload({
      bucket: dstBucket,
      key: dstObject,
    });
    console.log('UploadId', UploadId);

    // Get the size of existing objects in the source bucket.
    const {
      data: { 'content-length': contentLength },
    } = await client.headObject({
      bucket: srcBucket,
      key: srcObject,
    });
    console.log('srcObject content-length', contentLength);
    // Total file size
    const totalSize = contentLength;
    const partSize = 5 * 1024 * 1024;
    let offset = 0;
    let partNumber = 1;
    const partsInfo = [];

    while (offset < totalSize) {
      // Upload chunk copy
      const uploadResult = await client.uploadPartCopy({
        bucket: dstBucket,
        key: dstObject,
        partNumber,
        uploadId: UploadId,
        srcBucket,
        srcKey: srcObject,
        copySourceRangeStart: offset,
        copySourceRangeEnd: offset + partSize - 1,
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

    // Complete chunked upload.
    const { data } = await client.completeMultipartUpload({
      bucket: dstBucket,
      key: dstObject,
      uploadId: UploadId,
      parts: partsInfo,
    });
    console.log('result data:', data);

    // Query copy object information
    const headResult = await client.headObject({
      bucket: dstBucket,
      key: dstObject,
    });
    console.log('headResult', headResult);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="e9f779f9"></span>
## **Related documentation**


* For API documentation on creating a shard upload task, see [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on sharding copies, see [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy).

* For API documentation on merge sharding, see [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).
