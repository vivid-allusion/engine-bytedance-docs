---
title: "Deleting a Scenario (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-the-scenes-node-js-sdk"
---

This article introduces code examples for common object deletion scenarios.

<span id=".5Yig6Zmk55uu5b2V"></span>
## **Delete Directory**

The following code is used to delete objects in the specified directory `exampledir/`.

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
    const dir = 'exampledir/';
    for (let truncated = true, continuationToken = ''; truncated; ) {
      const { data } = await client.listObjectsType2({
        bucket: bucketName,
        maxKeys: 1000,
        continuationToken: continuationToken,
        prefix: dir,
      });

      for (const obj of data.Contents) {
        const { requestId } = await client.deleteObject({
          bucket: bucketName,
          key: obj.Key,
        });
        console.log('deleteObject %s Request ID:', obj.Key, requestId);
      }
      truncated = data.IsTruncated;
      continuationToken = data.NextContinuationToken;
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5riF56m65qG2"></span>
## **Empty Bucket**

The following code is used to empty the entire bucket, including deleting all objects and all unmerged objects.

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

    for (let isTruncated = true, continuationToken = ''; isTruncated; ) {
      const { data } = await client.listObjectsType2({
        maxKeys: 1000,
        bucket: bucketName,
        continuationToken,
      });

      for (const object of data.Contents) {
        const { requestId } = await client.deleteObject({
          bucket: bucketName,
          key: object.Key,
        });
        console.log('deleteObject %s Request ID:', object.Key, requestId);
      }

      isTruncated = data.IsTruncated;
      continuationToken = data.NextContinuationToken;
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


<span id=".5riF56m65byA5ZCv5aSa54mI5pys55qE5qG2"></span>
## **Emptying a versioned bucket**

The following is example code for clearing an entire multi\-version enabled bucket, including deleting all versions of objects, deleting all versions of delete markers, and deleting all unmerged objects.

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
