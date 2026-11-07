---
title: "Multi-Version Scenario (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Multi-version-scenarios-harmony-sdk"
---

Versioning is applied to all objects within the bucket. By enabling bucket versioning, you can restore objects to any previous version after accidental deletion or overwriting.

Currently, multi\-version support is available for interfaces including getObject, copyObject, uploadPartCopy, deleteObject, and others. When calling the relevant interfaces, you can specify the exact version of the target object by using the optional parameter `versionId`.

<span id="e7148872"></span>
## **Set Bucket Versioning Status**

In TOS, a bucket can be in one of three versioning states: versioning not enabled, versioning enabled, or versioning suspended. The following code demonstrates how to set the bucket status to either Enable (multi\-versioning enabled) or Suspended (versioning control suspended).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before configuring the bucket versioning status, you must have the <code>tos:PutBucketVersioning</code> permission.</div>


* <div data-tips="true" data-tips-type="warning">Before querying the bucket's versioning status, you must have the <code>tos:GetBucketVersioning</code> permission.</div>



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
    
    const res = await client.putBucketVersioning({
      Bucket: bucketName,
      Status: VersioningStatusType.VersioningStatusEnabled,
    });
    console.log('putBucketVersioning Request ID: ', res.RequestId);

    
    const res2 = await client.putBucketVersioning({
      Bucket: bucketName,
      Status: VersioningStatusType.VersioningStatusSuspended,
    });
    console.log('putBucketVersioning Request ID: ', res2.RequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="44469718"></span>
## **Download Versioned Objects**

The following code demonstrates how to download a specified version of a designated file from the harmonyos\-sdk\-test\-bucket and directly read and print the string in memory.

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
    
    const objectKey = '*** Provide your object key ***';
    
    const versionId = '*** Provide object Version ID ***';

    const res = await client.getObject({
      Bucket: bucketName,
      Key: objectKey,
      VersionId: versionId,
    });
    const content = buffer.from(res.Content.read(1000)).toString();
    res.Content.close();
    console.log('getObjectV2 Request ID: ', res.RequestId);
    console.log('buffer.length: ', content);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="4055a6bd"></span>
## **Deleting Multi\-Version Objects**

The following code demonstrates how to delete the specified version of a specified object in a bucket.

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
   
    const objectKey = '*** Provide your object key ***';
   
    const versionId = '*** Provide object Version ID ***';
 
    const res  = await client.deleteObject({
      Bucket: bucketName,
      Key: objectKey,
      VersionID: versionId,
    });
    console.log('deleteObject Request ID: ', res.RequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="0bde2730"></span>
## **Emptying a versioned bucket**

The following example code demonstrates how to completely clear a bucket with versioning enabled, including deleting all versions of all objects, deleting all versions of delete markers, and deleting all unmerged objects.

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
