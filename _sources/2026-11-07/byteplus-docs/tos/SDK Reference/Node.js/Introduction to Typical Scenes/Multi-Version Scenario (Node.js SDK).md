---
title: "Multi-Version Scenario (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Multi-version-scenes-node-js-sdk"
---

Versioning is applied to all objects in the bucket. By enabling bucket versioning, you can restore objects to any version from their history in the event of accidental deletion or overwrite.

Currently, the following interfaces support multi\-version functionality: getObjectV2, getObjectAcl, copyObject, uploadPartCopy, deleteObject, and others. When calling the relevant interfaces, you can specify the specific version of the object to operate on by using the optional parameter `versionId`.

<span id=".5qG25aSa54mI5pys566h55CG"></span>
## **Bucket Versioning Management**

In TOS, bucket versioning status includes three types: versioning not enabled, versioning enabled, and versioning suspended. This article introduces multi\-version management for buckets.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before setting the bucket versioning status, you must have the <code>tos:PutBucketVersioning</code> permission.</div>


* <div data-tips="true" data-tips-type="warning">Before querying the bucket's versioning status, you must have the <code>tos:GetBucketVersioning</code> permission.</div>



<span id=".6K6-572u5qG254mI5pys5o6n5Yi254q25oCB"></span>
### **Set Bucket Versioning Status**

```JavaScript
import { TosClient, TosClientError, TosServerError, VersioningStatusType } from '@volcengine/tos-sdk';

const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    const { requestId } = await client.putBucketVersioning({
      bucket: bucketName,
      status: VersioningStatusType.Enabled,
    });
    console.log('putBucketVersioning Request ID: ', requestId);

    const { requestId: requestId2 } = await client.putBucketVersioning({
      bucket: bucketName,
      status: VersioningStatusType.Suspended,
    });
    console.log('putBucketVersioning Request ID: ', requestId2);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5LiL6L295aSa54mI5pys5a-56LGh"></span>
### **Download Multi\-Version Objects**

```JavaScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    const objectKey = '*** Provide your object key ***';
    const versionId = '*** Provide object Version ID ***';
    const { data, requestId } = await client.getObjectV2({
      bucket: bucketName,
      dataType: 'buffer',
      key: objectKey,
      versionId,
    });
    console.log('getObjectV2 Request ID: ', requestId);
    console.log('buffer.length: ', data.content.length);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Yig6Zmk5aSa54mI5pys5a-56LGh"></span>
### **Deleting Multi\-Version Objects**

```JavaScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    const objectKey = '*** Provide your object key ***';
    const versionId = '*** Provide object Version ID ***';
    const { requestId } = await client.deleteObject({
      bucket: bucketName,
      key: objectKey,
      versionId,
    });
    console.log('deleteObject Request ID: ', requestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5riF56m65byA5ZCv5aSa54mI5pys55qE5qG2"></span>
### **Emptying a versioned bucket**

The following code sample is designed to clear an entire multi\-version bucket. It includes the deletion of all versions of all objects, the removal of all versions of delete markers, and the deletion of all unmerged objects.

```JavaScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
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
  try {
    const bucketName = 'node-sdk-test-bucket';

    for (let isTruncated = true, keyMarker = '', versionIdMarker = ''; isTruncated; ) {
      const { data } = await client.listObjectVersions({
        maxKeys: 1000,
        bucket: bucketName,
        keyMarker,
        versionIdMarker,
      });

      for (const object of data.Versions) {
        const { requestId } = await client.deleteObject({
          bucket: bucketName,
          key: object.Key,
          versionId: object.VersionId,
        });
        console.log('deleteObject %s Request ID:', object.Key, requestId);
      }

      for (const markers of data.DeleteMarkers) {
        const { requestId } = await client.deleteObject({
          bucket: bucketName,
          key: markers.Key,
          versionId: markers.VersionId,
        });
        console.log('deleteObject DeleteMarker %s Request ID:', markers.Key, requestId);
      }
      isTruncated = data.IsTruncated;
      keyMarker = data.NextKeyMarker;
      versionIdMarker = data.NextVersionIdMarker;
    }

    for (let isTruncated = true, keyMarker = '', uploadIdMarker = ''; isTruncated; ) {
      const { data } = await client.listMultipartUploads({
        bucket: bucketName,
        maxUploads: 1000,
        keyMarker,
        uploadIdMarker,
      });
      for (const upload of data.Uploads) {
        const { requestId } = await client.abortMultipartUpload({
          bucket: bucketName,
          key: upload.Key,
          uploadId: upload.UploadId,
        });
        console.log('abortMultipartUpload uploadId: %s, requestId: %s', upload.UploadId, requestId);
      }
      isTruncated = data.IsTruncated;
      keyMarker = data.NextKeyMarker;
      uploadIdMarker = data.NextUploadIdMarker;
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```
