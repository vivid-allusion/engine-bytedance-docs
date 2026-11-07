---
title: "Scenarios for Moving and Renaming (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Move-and-rename-scenes-node-js-sdk"
---

If you need to rename a file within a Bucket, you can use the CopyObject interface to copy the source object to the target object, and then use the DeleteObject interface to delete the source object.

<span id=".6YeN5ZG95ZCN5Y2V5Liq5a-56LGh"></span>
## **Renaming an Individual Object**

The following code is used to rename the object `src-object` in the bucket to `dest-object`.

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
    const srcObjectKey = 'src-object';
    const dstObjectKey = 'dest-object';

    const { requestId } = await client.copyObject({
      bucket: bucketName,
      key: dstObjectKey,
      srcBucket: bucketName,
      srcKey: srcObjectKey,
    });
    console.log('copyObject Request ID:', requestId);

    const { requestId: requestId2 } = await client.deleteObject({
      bucket: bucketName,
      key: srcObjectKey,
    });
    console.log('deleteObject Request ID:', requestId2);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6YeN5ZG95ZCN55uu5b2V"></span>
## **Rename Directory**

The following code is used to rename the directory `exampledir1/` to `exampledir2/` within the specified storage bucket.

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
    const srcDir = 'exampledir1/';
    const dstDir = 'exampledir2/';

    for (let truncated = true, continuationToken = ''; truncated; ) {
      const { data } = await client.listObjectsType2({
        bucket: bucketName,
        maxKeys: 1000,
        continuationToken: continuationToken,
        prefix: srcDir,
      });

      for (const obj of data.Contents) {
        const { requestId } = await client.copyObject({
          bucket: bucketName,
          key: obj.Key.replace(srcDir, dstDir),
          srcBucket: bucketName,
          srcKey: obj.Key,
        });
        console.log('copyObject %s Request ID:', obj.Key, requestId);
        const { requestId: requestId2 } = await client.deleteObject({
          bucket: bucketName,
          key: obj.Key,
        });
        console.log('deleteObject %s Request ID:', obj.Key, requestId2);
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
