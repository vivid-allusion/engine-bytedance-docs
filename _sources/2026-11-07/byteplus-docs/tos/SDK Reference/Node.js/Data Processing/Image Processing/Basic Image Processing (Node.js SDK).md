---
title: "Basic Image Processing (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Basic-image-processing-node-js-sdk"
---

TOS supports image processing, including image scaling, image cropping, image watermarking, format conversion and other image processing operations. This article describes how to perform basic image processing through the TOS Node.js SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The original image format only supports JPG, PNG, BMP, GIF, WEBP, and TIFF.

* The size of the original image cannot exceed 20MB.

* The width and height of the original image cannot exceed 30000 px, and the total pixels cannot exceed 250 million px (the width and height of the original image for rotation operation cannot exceed 4096 px).

* The width and height of the scaled image cannot exceed 16384 px, and the total pixels cannot exceed 16777216 px.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code shows how to fix the image height to 100px, convert the image format to JPG format, and then name the image temp.jpg and download it locally.

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
    // Save to file
    const fileName = 'temp.jpg';
    // Request and add data processing
    const style = 'image/resize,h_100/format,jpg'; /* Fix the image height to 100px and convert it to JPG format. */
    const { requestId, headers } = await client.getObjectToFile({
      bucket: bucketName,
      key: imageKey,
      process: style,
      filePath: fileName,
    });
    console.log('getObjectToFile Request ID: ', requestId);
    console.log('ContentType: ', headers['content-type']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to image processing, please refer to [Image Processing Overview](https://docs.byteplus.com/docs/tos/docs-overview_2).
