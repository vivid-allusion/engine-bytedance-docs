---
title: "Deleting a Bucket (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-bucket-node-js-sdk"
---

When you no longer need to keep a bucket, you can delete it to avoid incurring additional charges.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Precautions


* After the bucket is deleted, it cannot be recovered. Please proceed with caution.

* Before you can delete a bucket, you must have the `tos: DeleteBucket`permission. For specific operations, please refer to [Overview](https://docs.byteplus.com/docs/tos/docs--overview)


<span id="41931586"></span>
## Prerequisite

Before deleting a bucket, make sure you have deleted all the data in the bucket.


* If the bucket has version control turned on, make sure that all current version and history objects in the current bucket have been deleted. For specific operations, please refer to [Permanently deleting a file](https://docs.byteplus.com/docs/tos/docs-versioning-related-operations#455328aa).

* If there are unmerged shardings in the bucket, make sure to delete all sharding data for specific operations. Please see [Managing Parts](https://docs.byteplus.com/docs/tos/docs-managing-parts).

* If there are many objects in the bucket, you can set the bulk deletion of objects through the life cycle rule. For specific operations, please refer to [Setting Lifecycle Rules](https://docs.byteplus.com/docs/tos/docs-setting-lifecycle-rules).


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
    // Check if the bucket exists.
    const { data } = await client.deleteBucket(bucketName);
    console.log(`the result of delete ${bucketName} is`, data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="444507e0"></span>
## Related documentation

For API documentation on deleting buckets, see [DeleteBucket](https://docs.byteplus.com/docs/tos/reference-deletebucket).
