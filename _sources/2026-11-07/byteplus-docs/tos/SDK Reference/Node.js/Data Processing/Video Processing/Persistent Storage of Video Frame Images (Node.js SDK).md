---
title: "Persistent Storage of Video Frame Images (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-capture-image-persistence-node-js-sdk"
---

TOS supports saving the picture after the video frame to the specified storage bucket. This article describes how to save the image of the video frame to the specified bucket through the TOS Node.js SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code shows how to capture the 300ms video frame, name the captured image temp.jpg, and save it to the destination bucket.

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
    // Video name
    const videoKey = 'video.mp4';
    // Specify the name of the storage bucket to save the processed images
    const saveBucket = '*** Provide your bucket name ***';
    // Specify the name of the processed image
    const saveObject = 'temp.jpg';

    // Request and add data processing
    const style = 'video/snapshot,t_300'; /* Video frame capture, capture the video frame at 300ms.*/
    const { data, requestId, headers } = await client.getObjectV2({
      bucket: bucketName,
      key: videoKey,
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

For a detailed introduction to the persistence of video screenshots, see [Image Storage](https://docs.byteplus.com/docs/tos/docs-image-storage).
