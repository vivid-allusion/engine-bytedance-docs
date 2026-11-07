---
title: "Managing Object Tags (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-tags-node-js-sdk"
---

TOS supports setting custom tags for objects, and completes the life cycle management of specific objects according to the object tags. This article describes how to manage object tags through the TOS Node.js SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* To set the object tag, you must have the `tos: PutObjectTagging`permission, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* To get the object tag, you must have `tos: GetObjectTagging`permission, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* To remove an object tag, you must have `tos: DeleteObjectTagging`permission,see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* Each object can add up to 10 tags, and the keys of the same object cannot be repeated. For a description of the restrictions on object tags, see [Managing File Tags](https://docs.byteplus.com/docs/tos/docs-managing-file-labels).


<span id=".6K6-572u5a-56LGh5qCH562-"></span>
## **Set object tag**

```JavaScript
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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    // The specified objectKey.
    const objectKey = '*** Provide your object key ***';

    const { requestId } = await client.putObjectTagging({
      bucket: bucketName,
      key: objectKey,
      tagSet: {
        Tags: [
          { Key: 'tagA', Value: 'valueA' },
          { Key: 'tagB', Value: 'valueB' },
        ],
      },
    });
    console.log('putObjectTagging Request ID:', requestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6I635Y-W5a-56LGh5qCH562-"></span>
## **Get object tag**

After setting the object tag, you can obtain the tag information of the object.

```JavaScript
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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    // The specified objectKey.
    const objectKey = '*** Provide your object key ***';

    const { data, requestId } = await client.getObjectTagging({
      bucket: bucketName,
      key: objectKey,
    });
    console.log('getObjectTagging Request ID:', requestId);
    console.log('getObjectTagging Tags.length:', data.TagSet.Tags.length);
    for (const tag of data.TagSet.Tags) {
      console.log('Tag Key:', tag.Key);
      console.log('Tag Value:', tag.Value);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Yig6Zmk5a-56LGh5qCH562-"></span>
## **Delete object tag**

```JavaScript
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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    // The specified objectKey.
    const objectKey = '*** Provide your object key ***';

    const { requestId } = await client.deleteObjectTagging({
      bucket: bucketName,
      key: objectKey,
    });
    console.log('deleteObjectTagging Request ID:', requestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information on object tags, see [Managing File Tags](https://docs.byteplus.com/docs/tos/docs-managing-file-labels).
