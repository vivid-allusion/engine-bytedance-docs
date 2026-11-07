---
title: "Image Processing Persistence (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Image-processing-persistence-node-js-sdk"
---

TOS does not save processed images by default. You can use the code to save the processed image to the specified bucket. This article describes how to save the processed image to the specified bucket through the TOS Node.js SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The account that uses image processing persistence must have the read permission of the bucket where the original image is located, and the write permission of the target bucket where the image is dumped.

* When using an anonymous user to save a processed image to a specified bucket, that bucket must have public write permissions.

* The original image bucket and the image dump target bucket must belong to the same region.

* Access to dumped images defaults to private, and storage type defaults to standard storage.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code shows how to fix the image height to 100px, convert the image format to JPG format, and then name the processed image temp.jpg and save it to the target bucket.

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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    // Original image name
    const imageKey = 'image.png';
    // Specify the name of the storage bucket to save the processed image
    const saveBucket = '*** Provide your bucket name ***';
    // Specify the name of the processed image
    const saveObject = 'temp.jpg';

    // Request and add data processing
    const style = 'image/resize,h_100/format,jpg'; /* Fix the image height to 100px and convert it to JPG format. */
    const { data, requestId, headers } = await client.getObjectV2({
      bucket: bucketName,
      key: imageKey,
      process: style,
      dataType: 'buffer',
      saveBucket: Buffer.from(saveBucket).toString('base64url'),
      saveObject: Buffer.from(saveObject).toString('base64url'),
    });

    console.log('getObjectV2 Request ID: ', requestId);
    console.log('ContentType: ', headers['content-type']);
    const info = JSON.parse(data.content.toString());
    console.log('Save As Result: %o', info);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to image processing persistence, see [Image Storage](https://docs.byteplus.com/docs/tos/docs-image-storage).
