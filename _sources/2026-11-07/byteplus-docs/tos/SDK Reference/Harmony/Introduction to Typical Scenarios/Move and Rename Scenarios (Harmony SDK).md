---
title: "Move and Rename Scenarios (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Move-and-rename-scenarios-harmony-sdk"
---

If you need to rename a file within a Bucket, you can use the CopyObject interface to copy the source object to the target object, and then use the DeleteObject interface to delete the source object.

<span id="5d65fb24"></span>
## **Renaming an Individual Object**

The following code is used to rename the object `src-object` in the bucket to `dest-object`.

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
    const srcObjectKey = 'src-object';
    const dstObjectKey = 'dest-object';

    
    const res = await client.copyObject({
      Bucket: bucketName,
      Key: dstObjectKey,
      SrcBucket: bucketName,
      SrcKey: srcObjectKey,
    });
    console.log('copyObject Request ID:', res.RequestId);

    
    const res2 = await client.deleteObject({
      Bucket: bucketName,
      Key: srcObjectKey,
    });
    console.log('deleteObject Request ID:', res2.RequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="badc7379"></span>
## **Rename Directory**

The following code is used to rename the directory `exampledir1/` to `exampledir2/` within the specified storage bucket.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

async function main() {
  try {
    const srcDir = 'exampledir1/';
    const dstDir = 'exampledir2/';
    let continuationToken = '';

    while (true) {
      const res = await client.listObjectsType2({
        Bucket: bucketName,
        MaxKeys: 1000,
        ContinuationToken: continuationToken,
        Prefix: srcDir,
      });

      for (const obj of res.Contents) {
       
        const res2 = await client.copyObject({
          Bucket: bucketName,
          Key: obj.Key.replace(srcDir, dstDir),
          SrcBucket: bucketName,
          SrcKey: obj.Key,
        });
        console.log('copyObject %s Request ID:', obj.Key, res2.RequestId);
        
        const res3 = await client.deleteObject({
          Bucket: bucketName,
          Key: obj.Key,
        });
        console.log('deleteObject %s Request ID:', obj.Key, res3.RequestId);
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
