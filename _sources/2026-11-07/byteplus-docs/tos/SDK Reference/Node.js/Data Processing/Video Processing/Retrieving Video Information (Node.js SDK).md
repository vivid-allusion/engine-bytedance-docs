---
title: "Retrieving Video Information (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-video-information-node-js-sdk"
---

The Get Video Information function can obtain meta information for a specified video resource. This article describes how to obtain video information through the TOS Node.js SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code shows how to obtain video information.

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
    // Video Title
    const videoKey = 'video.mp4';

    const style = 'video/info'; /* Get video information. */
    const { data, requestId, headers } = await client.getObjectV2({
      bucket: bucketName,
      key: videoKey,
      dataType: 'buffer',
      process: style,
    });
    console.log('getObjectV2 Request ID: ', requestId);
    console.log('ContentType: ', headers['content-type']);

    const info = JSON.parse(data.content.toString());
    console.log('info: %o', info);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For details on obtaining video information, see [Viewing Video Information](https://docs.byteplus.com/docs/tos/docs-viewing-video-information).
