---
title: "Abnormal Image Detection (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Abnormal-image-detection-node-js-sdk"
---

Anomalous image detection is used to detect whether an image contains any suspicious files other than images, such as MPEG\-TS files. If it is detected that the image contains a suspicious file, you can process the image file to prevent the storage space from being illegally stolen. This article describes how to detect abnormal images through the TOS Node.js SDK.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The size of the detected original image cannot exceed 20MB.

* Only abnormal image detection is supported for JPG, JPEG, PNG, BMP, GIF, and pure TS video stream format files.

* The abnormal picture detection function is billed according to the number of times it is processed. For detailed instructions, please refer to [Data Processing Fee](https://docs.byteplus.com/docs/tos/docs-data-processing-fee).


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code shows how to detect abnormal images.

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
    // Image Name
    const imageKey = 'image.png';

    const style = 'image/inspect'; /* Abnormal image detection */
    const { data, requestId, headers } = await client.getObjectV2({
      bucket: bucketName,
      key: imageKey,
      dataType: 'buffer',
      process: style,
    });
    console.log('getObjectV2 Request ID: ', requestId);
    console.log('ContentType: ', headers['content-type']);

    const info = JSON.parse(data.content.toString());
    console.log('picSize: ', info.picSize);
    console.log('picType: ', info.picType);
    console.log('suspicious: ', info.suspicious);
  } catch (error) {
    handleError(error);
  }
}

main();
```
