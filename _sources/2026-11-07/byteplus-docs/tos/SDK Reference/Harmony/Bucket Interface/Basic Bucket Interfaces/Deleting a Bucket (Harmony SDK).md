---
title: "Deleting a Bucket (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-bucket-harmony-sdk"
---

When you no longer need to retain a bucket (Bucket), you may delete it to avoid incurring additional charges.

<span id="d67548aa"></span>
## Precautions


* Once a bucket is deleted, it cannot be restored. Please proceed with caution.

* Before deleting a bucket, you must have the `tos:DeleteBucket` permission.


<span id="368374e3"></span>
## Prerequisites

Before deleting a bucket, ensure that all data within the bucket has been removed.


* If versioning is enabled for the bucket, please ensure that all current and historical version objects within the bucket have been deleted. For detailed instructions, see [Delete Object](https://docs.byteplus.com/docs/tos/docs-versioning-related-operations#%E5%BD%BB%E5%BA%95%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6).

* If there are unmerged fragments in the bucket, ensure that all fragment data is deleted. Specific operations: See [Delete Shard](https://docs.byteplus.com/docs/tos/docs-managing-parts#%E5%88%A0%E9%99%A4%E5%88%86%E7%89%87).

* If a bucket contains a large number of objects, you can configure lifecycle rules to enable batch deletion of objects. For detailed instructions, see [Setting Lifecycle Rules](https://docs.byteplus.com/docs/6349/75028).


<span id="92f9e330"></span>
## Sample Code

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak', 
  accessKeySecret: "Provide your ak", 
  securityToken: 'Provide your securityToken',
  region: "Provide your region",
  endpoint: "Provide your endpoint", 
});

function handleError(error: Error) {
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

    const res = await client.deleteBucket({
      Bucket: bucketName
    });
    console.log(`the status code of delete ${bucketName} is`, res.StatusCode);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="9906942e"></span>
## Relevant Documentation

For API documentation on deleting a bucket, see [DeleteBucket](https://docs.byteplus.com/docs/tos/reference-deletebucket).
