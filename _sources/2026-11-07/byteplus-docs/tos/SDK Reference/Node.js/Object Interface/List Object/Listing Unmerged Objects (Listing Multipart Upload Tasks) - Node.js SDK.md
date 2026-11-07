---
title: "Listing Unmerged Objects (Listing Multipart Upload Tasks) - Node.js SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-unmerged-objects-node-js-sdk"
---

This interface is used to enumerate the unmerged objects in the bucket, that is, to enumerate the shard upload task.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Before listing the shard upload tasks, you need to have the `tos: ListBucketMultipartUploads`permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description


|parameter |describe |
|---|---|
|delimiter |Characters to group object names. |
|encodingType |Encodes the returned content and specifies the type of encoding. The value selection description is as follows:<br><br><br>* `Undefined`: Default value, no encoding.<br><br>* `'Url '`: Encode the URL. |
|maxUploads |Returns the maximum number of shard upload tasks. The default value is 1000.<br><br>Value: (0, 1000] |
|prefix |Used to specify the prefix name of the enumerated returned object. |
|keyMarker |List the starting position of the shard upload task. Sets to return a list of objects sorted alphabetically from the value. Usually the `nextMarker`value returned by the last request. |
|uploadIDMarker |Used with `keyMarker`, set to return a sharded upload task list sorted by dictionary from this value. Gets the `nextVersionIdMarker`from the last enumeration. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".566A5Y2V5YiX5Li-"></span>
### Simple list

The following code enumerates up to 10 unmerged shard upload tasks in the specified bucket.

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
    // Get up to 10 unfinished tasks from the bucket.
    const { data } = await client.listMultipartUploads({
      bucket: bucketName,
      maxKeys: 1000,
    });

    console.log('Uploads.length:', data.Uploads.length);
    for (const upload of data.Uploads) {
      console.log('Object Key:', upload.Key);
      console.log('UploadID:', upload.UploadId);
      console.log('Owner:', upload.Owner);
      console.log('StorageClass:', upload.StorageClass);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5pyq5ZCI5bm255qE5YiG54mH5Lu75Yqh"></span>
### List all unmerged sharding tasks with the specified prefix

The following code enumerates all unmerged shard upload tasks under the specified bucket prefix.

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
    // List all multi-version objects with the specified prefix.
    const prefix = '*** Provide your object key prefix ***';
    for (let truncated = true, keyMarker = '', uploadIdMarker = ''; truncated; ) {
      const { data } = await client.listMultipartUploads({
        bucket: bucketName,
        maxUploads: 1000,
        prefix,
        keyMarker,
        uploadIdMarker,
      });

      console.log('Uploads.length:', data.Uploads.length);
      for (const upload of data.Uploads) {
        console.log('Object Key:', upload.Key);
        console.log('UploadID:', upload.UploadId);
        console.log('Owner:', upload.Owner);
        console.log('StorageClass:', upload.StorageClass);
      }

      truncated = data.IsTruncated;
      keyMarker = data.NextKeyMarker;
      uploadIdMarker = data.NextUploadIdMarker;
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5YiX5Li-5omA5pyJ5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### List all shard upload tasks

The following code enumerates all shard upload tasks for which buckets are not merged.

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
    // List all multi-version objects.
    for (let truncated = true, keyMarker = '', uploadIdMarker = ''; truncated; ) {
      const { data } = await client.listMultipartUploads({
        bucket: bucketName,
        maxUploads: 1000,
        keyMarker,
        uploadIdMarker,
      });

      console.log('Uploads.length:', data.Uploads.length);
      for (const upload of data.Uploads) {
        console.log('Object Key:', upload.Key);
        console.log('UploadID:', upload.UploadId);
        console.log('Owner:', upload.Owner);
        console.log('StorageClass:', upload.StorageClass);
      }

      truncated = data.IsTruncated;
      keyMarker = data.NextKeyMarker;
      uploadIdMarker = data.NextUploadIdMarker;
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```
