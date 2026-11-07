---
title: "Exception Handling (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Exception-handling-browser-js-sdk"
---

This article presents exception handling when using the TOS SDK.

<span id=".dG9zLeacjeWKoeerr-mUmeivrw=="></span>
## TOS Server\-Side Error

The TOS server complies with HTTP specifications and defines detailed HTTP status codes and business error codes for scenarios involving request failures. For detailed information, please refer to [TOS Server-Side Status Codes and Error Codes Definition](https://docs.byteplus.com/en/docs/tos/reference-codes-in-response).

<span id=".c2RrLeiHquWumuS5iemUmeivrw=="></span>
## SDK Custom Errors

<span id=".5a6i5oi356uv6ZSZ6K-vLXRvc2NsaWVudGVycm9y"></span>
### Client Error \- TosClientError

TosClientError is caused by incorrect client input parameters, connection timeouts, or special client operations such as canceling a resumable upload and other similar actions. For example, when creating a bucket using CreateBucketV2, an exception is thrown if the bucket name exceeds 63 characters in length.

<span id=".5pyN5Yqh56uv6ZSZ6K-vLXRvc3NlcnZlcmVycm9y"></span>
### Server\-Side Error \- TosServerError

Requests are sent to the TOS server via the TOS SDK interface. The response to each request includes status codes that comply with HTTP standards and business error codes, which indicate the response status of the current request.

<span id=".6ZSZ6K-v5aSE55CG56S65L6L"></span>
### Error Handling Examples

The following code demonstrates exception handling when attempting to download a non\-existent object.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <button id="download">Download</button>
    <script src="https://tos-public.volccdn.com/obj/volc-tos-public/@volcengine/tos-sdk@latest/browser/tos.umd.production.min.js"></script>
    <script type="text/javascript">
      const { TosClientError, TosServerError } = TosClient;
      const client = new TosClient({
        region: yourRegion,
        endpoint: yourEndpoint,
        accessKeyId: yourAccessKey,
        accessKeySecret: yourSecretKey,
        stsToken: yourSecurityToken,
        bucket: examplebucket,
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
      
      const download = document.getElementById('download');
      download.addEventListener('click', async () => {
        try {
          await client.getObjectV2({
            key: 'exampledir/notExistObjct.txt',
            dataType: 'blob',
          });
        } catch (error) {
          handleError(error);
        }
      });
    </script>
  </body>
</html>
```
