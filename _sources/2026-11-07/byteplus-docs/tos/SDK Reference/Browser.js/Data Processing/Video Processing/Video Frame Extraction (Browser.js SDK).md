---
title: "Video Frame Extraction (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-framing-browser-js-sdk"
---

The video frame capture function enables extraction of a single frame from a video stream at a specified time and resizes it to a designated image size. This article describes how to perform video frame capture using the TOS Browser.js SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to extract the video frame at 300 milliseconds and display it on a webpage.

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Video frame capture</title>
  </head>

  <body>
    <img src="" style="width: 300px; height: 300px" />
    <script src="https://cdn.jsdelivr.net/npm/@volcengine/tos-sdk@latest/browser/tos.umd.production.min.js"></script>
    <script type="text/javascript">
      const { TosClientError, TosServerError } = TosClient;
      const client = new TosClient({
        region: 'yourRegion',
        accessKeyId: 'yourAccessKeyId',
        accessKeySecret: 'yourAccessKeySecret',
        stsToken: 'yourSecurityToken',
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
          const videoKey = 'video.mp4';
          const fileName = 'temp.jpg';
          const style = 'video/snapshot,t_300';
          const { data, requestId, headers } = await client.getObjectV2({
            bucket: bucketName,
            key: videoKey,
            process: style,
            dataType: 'blob',
          });
          console.log('getObjectToFile Request ID: ', requestId);
          console.log('ContentType: ', headers['content-type']);
          const imageUrl = window.URL.createObjectURL(data.content);
          document.querySelector('img').src = imageUrl;
        } catch (error) {
          handleError(error);
        }
      }
      main();
    </script>
  </body>
</html>
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to video frame extraction, please refer to [Video Frame Extraction](https://docs.byteplus.com/docs/tos/docs-video-frame-capture).
