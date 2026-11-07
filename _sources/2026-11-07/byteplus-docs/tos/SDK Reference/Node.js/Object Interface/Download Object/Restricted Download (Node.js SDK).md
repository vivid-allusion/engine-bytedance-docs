---
title: "Restricted Download (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Limited-download-node-js-sdk"
---

If you want to set restrictions on downloading objects (object ETag or object modification time) when downloading objects, you can use the restricted download function provided by the TOS Node.js SDK to download objects only when the object information meets the conditions you specify. This article describes how to download objects by qualifying them.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before downloading an object, you must have `tos: GetObject`permission, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* To open multiple versions of the bucket, when downloading the specified version object, you must have the `tos: GetObjectVersion`permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* If an application downloads a large number of the same object at the same time, your access speed will be limited by TOS bandwidth and geography. It is recommended that you use CDN products to improve performance while also reducing your costs.

* Different conditions can be combined, for example: If\-Modified\-Since and If\-Unmodified\-Since can coexist, if\-Match and If\-One\-Match can also coexist.

* Object Etag information can be obtained by using the **headObject** interface of the TOS Node.js SDK.


<span id=".6ZmQ5a6a5p2h5Lu26K-05piO"></span>
## Qualification statement


|parameter |describe |
|---|---|
|If\-Match |An object is returned only if the incoming `ETag`is equal to the object's `ETag`, otherwise `412 Precondition Failed`is returned. |
|If\-None\-Match |An object is returned only if the incoming `ETag`is not equal to the object's `ETag`, otherwise `304 Not Modified`is returned. |
|If\-Modified\-Since |The object is returned only if it has been modified since the specified time, otherwise `304 Not Modified`is returned. |
|If\-Unmodified\-Since |The object is returned only if it has not been modified since the specified time, otherwise `412 Precondition Failed`is returned. |


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

async function main() {
  const bucketName = 'node-sdk-test-bucket'; // Target bucket
  const objectName = 'example_dir/example.txt'; // Target object
  // Specify a date as a download criterion.
  const date = new Date('2024-02-22 18:33:00');

  try {
    // Get object
    const res = await client.getObjectV2({
      bucket: bucketName,
      key: objectName,
      ifModifiedSince: date,
    });

    // When the specified conditions are met, read the object.
    let allContent = Buffer.from([]);
    for await (const chunk of res.data.content) {
      allContent = Buffer.concat([allContent, chunk]);
    }
    console.log('object size:', allContent.length);
    // If the object is a string, it can be parsed using toString.
    console.log('data string:', allContent.toString());
  } catch (error) {
    if (error instanceof TosServerError) {
      // IfModifiedSince is not satisfied, return 304.
      if (error.statusCode === 304) {
        console.log('Object not modify, Request ID:', error.requestId);
      } else {
        handleError(error);
      }
    }
  }

  try {
    // Get object
    const {
      data: { content },
    } = await client.getObjectV2({
      bucket: bucketName,
      key: objectName,
      ifUnmodifiedSince: date,
    });

    // When the specified conditions are met, read the object.
    let allContent = Buffer.from([]);
    for await (const chunk of content) {
      allContent = Buffer.concat([allContent, chunk]);
    }
    console.log('object size:', allContent.length);
    // If the object is a string of text, it can be parsed using toString.
    console.log('data string:', allContent.toString());
  } catch (error) {
    if (error instanceof TosServerError) {
      // If the resource has not been modified since the specified date and time, return 412.
      if (error.statusCode === 412) {
        console.log('Object modify, Request ID:', error.requestId);
      } else {
        handleError(error);
      }
    }
  }
}

main();
```


<span id="12074890"></span>
## **Related documentation**

For API documentation on downloading objects, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
