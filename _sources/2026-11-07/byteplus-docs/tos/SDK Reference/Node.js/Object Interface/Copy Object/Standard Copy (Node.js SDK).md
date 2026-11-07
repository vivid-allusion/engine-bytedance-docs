---
title: "Standard Copy (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-copy-node-js-sdk"
---

With copyObject, you can copy objects between buckets in the same region, or within the same bucket. When copying, you can specify new metadata information or maintain metadata information for the source object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Copy files do not support inter\-barrel copying across regions.

* When copying an object, the account must have read access to the source object and write access to the destination bucket.

* When copying an object, you can either preserve all metadata (the default) or specify new metadata. However, the ACL is not preserved, but is set to private.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code shows how to copy the object srcObject from the bucket srcBucket to the object dstObject in the bucket dstBucket via copyObject.

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { ACLType, MetadataDirectiveType, StorageClassType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

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

    // Copy an object within the same bucket, using the original metadata.
    const { data } = await client.copyObject({
      bucket: srcBucket,
      key: dstObject,
      srcBucket,
      srcKey: srcObject,
      metadataDirective: MetadataDirectiveType.MetadataDirectiveCopy,
    });
    console.log('copy result', data);
    // Query copy object information.
    const headResult = await client.headObject({
      bucket: dstBucket,
      key: dstObject,
    });
    console.log('headResult', headResult);

    // Copy the object using the specified metadata information.
    const { data: data2 } = await client.copyObject({
      bucket: dstBucket,
      key: dstObject,
      srcBucket,
      srcKey: srcObject,
      metadataDirective: MetadataDirectiveType.MetadataDirectiveReplace,
      // Specify the object as low-frequency storage when copying
      storageClass: StorageClassType.StorageClassIa,
      // Specify private permissions when copying
      acl: ACLType.ACLPrivate,
      // Set meta metadata when copying
      meta: { key: 'value' },
    });
    console.log('copy result', data2);
    // Query copy object information.
    const headResult2 = await client.headObject({
      bucket: dstBucket,
      key: dstObject,
    });
    console.log('headResult', headResult2);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="6fa8c2c8"></span>
## **Related documentation**

For API documentation on normal copy, see [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).
