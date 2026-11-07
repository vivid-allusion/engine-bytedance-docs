---
title: "Retrieving Video Information (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-video-information-browser-js-sdk"
---

The video information retrieval function enables access to the metadata of a specified video resource. This article describes how to obtain video information using the TOS Browser.js SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to retrieve video information.

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Get video information</title>
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

          const style = 'video/info'; 
          const { data, requestId, headers } = await client.getObjectV2({
            bucket: bucketName,
            key: videoKey,
            process: style,
            dataType: 'blob',
          });
          console.log('getObjectV2 Request ID: ', requestId);
          console.log('ContentType: ', headers['content-type']);

          const info = JSON.parse(await data.content.text());
          console.log('info: %o', info);
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

For a detailed introduction to obtaining video information, please refer to [Video Information Guide](https://docs.byteplus.com/docs/tos/docs-viewing-video-information).
