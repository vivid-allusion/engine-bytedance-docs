---
title: "Persistent Storage of Video Frame Images (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-capture-image-persistence-browser-js-sdk"
---

TOS supports saving images extracted from video frames to a specified storage bucket. This article explains how to use the TOS Browser.js SDK to save images captured from video frames to a specified storage bucket.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to extract the video frame at 300 milliseconds, name the resulting image temp.jpg, and save it to the target storage bucket.

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Video frame image persistence</title>
  </head>

  <body>
    <div>Please see console for more information</div>
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
          const saveBucket = '*** Provide your bucket name ***';
          const saveObject = 'temp.jpg';
          
          const style = 'video/snapshot,t_300';
          const { data, requestId, headers } = await client.getObjectV2({
            bucket: bucketName,
            key: videoKey,
            process: style,
            dataType: 'blob',
            saveBucket: btoa(saveBucket),
            saveObject: btoa(saveObject),
          });

          console.log('getObjectV2 Request ID: ', requestId);
          console.log('ContentType: ', headers['content-type']);
          const info = JSON.parse(await data.content.text());
          console.log('Save As Result: %o', info);
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

For a detailed introduction to the persistence of images captured from video frames, please refer to [Image Persistence](https://docs.byteplus.com/docs/tos/docs-image-storage).
