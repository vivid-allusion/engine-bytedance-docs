---
title: "Determining Whether an Object Exists (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Determine-whether-an-object-exists-node-js-sdk"
---

You can determine whether an object exists through the `headObject`interface of the Node.js SDK.

<span id="555b6737"></span>
## Precautions

To determine whether the object exists, your account must have the `tos: GetObject`permission, see the specific operation [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

<span id="480f20d1"></span>
## Sample code

The following code shows how to determine whether an object exists.

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
    // Object name in the storage bucket.
    const objectKey = 'example_dir/example.txt';

    const { requestId } = await client.headObject({
      bucket: bucketName,
      key: objectKey,
    });
    console.log('The object exists.');
    console.log('headObject Request ID:', requestId);
  } catch (error) {
    if (error instanceof TosServerError) {
      if (error.statusCode === 404) {
        // The object does not exist.
        console.log(`The object doesn't exist`);
        return;
      }
    }

    handleError(error);
  }
}

main();
```


<span id="8154434b"></span>
## **Related documentation**

For an API interface to determine whether an object exists, see [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject).
