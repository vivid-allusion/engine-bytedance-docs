---
title: "Deleting a Scene (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Deletion-scenarios-harmony-sdk"
---

This article introduces code examples for common object deletion scenarios.

<span id="f0524539"></span>
## **Delete Directory**

The following code is used to delete objects in the specified directory `exampledir/`.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
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

const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {
  try {
   
    const dir = 'exampledir/';
    let continuationToken = '';
    while (true) {
      const res = await client.listObjectsType2({
        Bucket: bucketName,
        MaxKeys: 1000,
        ContinuationToken: continuationToken,
        Prefix: dir,
      });

      for (const obj of res.Contents) {
        const res2 = await client.deleteObject({
          Bucket: bucketName,
          Key: obj.Key,
        });
        console.log('deleteObject %s Request ID:', obj.Key, res2.RequestId);
      }
      if (!res.IsTruncated) {
        break;
      }
      continuationToken = res.NextContinuationToken ?? '';
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="92985e49"></span>
## **Empty Bucket**

The following code is used to clear the entire bucket, including deleting all objects and all unmerged objects.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
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
    let continuationToken = '';
    while (true) {
      const res = await client.listObjectsType2({
        Bucket: bucketName,
        MaxKeys: 1000,
        ContinuationToken: continuationToken,
      });

      for (const obj of res.Contents) {
        const res2 = await client.deleteObject({
          Bucket: bucketName,
          Key: obj.Key,
        });
        console.log('deleteObject %s Request ID:', obj.Key, res2.RequestId);
      }
      if (!res.IsTruncated) {
        break;
      }
      continuationToken = res.NextContinuationToken ?? '';
    }
    let keyMarker2 = '';
    let uploadIdMarker = '';
    
    while (true) {
      const res = await client.listMultipartUploads({
        Bucket: bucketName,
        MaxUploads: 1000,
        KeyMarker: keyMarker2,
        UploadIdMarker: uploadIdMarker,
      });
      for (const upload of res.Uploads) {
        const res2 = await client.abortMultipartUpload({
          Bucket: bucketName,
          Key: upload.Key,
          UploadID: upload.UploadId,
        });
        console.log('abortMultipartUpload uploadId: %s, requestId: %s', upload.UploadId, res2.RequestId);
      }
      if (!res.IsTruncated) {
        break;
      }
      keyMarker2 = res.NextKeyMarker ?? '';
      uploadIdMarker = res.NextUploadIdMarker ?? '';
    }
    
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="d1ba60fd"></span>
## **Emptying a versioning\-enabled bucket**

The following code provides an example for clearing an entire bucket with versioning enabled, including deleting all versions of objects, all versions of delete markers, and all incomplete multipart uploads.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
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
    const bucketName = 'harmonyos-sdk-test-bucket';

 
    let keyMarker = '';
    let versionIdMarker = '';
    while (true) {
      const res = await client.listObjectVersions({
        MaxKeys: 1000,
        Bucket: bucketName,
        KeyMarker: keyMarker,
        VersionIDMarker: versionIdMarker,
      });

      
      for (const object of res.Versions) {
        const res2 = await client.deleteObject({
          Bucket: bucketName,
          Key: object.Key,
          VersionID: object.VersionId,
        });
        console.log('deleteObject %s Request ID:', object.Key, res2.RequestId);
      }


      for (const markers of res.DeleteMarkers) {
        const res2 = await client.deleteObject({
          Bucket: bucketName,
          Key: markers.Key,
          VersionID: markers.VersionId,
        });
        console.log('deleteObject DeleteMarker %s Request ID:', markers.Key, res2.RequestId);
      }
      if (!res.IsTruncated) {
        break;
      }
      keyMarker = res.NextKeyMarker ?? '';
      versionIdMarker = res.NextVersionIdMarker ?? '';
    }

    let keyMarker2 = '';
    let uploadIdMarker = '';

    while (true) {
      const res = await client.listMultipartUploads({
        Bucket: bucketName,
        MaxUploads: 1000,
        KeyMarker: keyMarker2,
        UploadIdMarker: uploadIdMarker,
      });
      for (const upload of res.Uploads) {
        const res2 = await client.abortMultipartUpload({
          Bucket: bucketName,
          Key: upload.Key,
          UploadID: upload.UploadId,
        });
        console.log('abortMultipartUpload uploadId: %s, requestId: %s', upload.UploadId, res2.RequestId);
      }
      if (!res.IsTruncated) {
        break;
      }
      keyMarker = res.NextKeyMarker ?? '';
      uploadIdMarker = res.NextUploadIdMarker ?? '';
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```
