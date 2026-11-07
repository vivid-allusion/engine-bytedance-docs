---
title: "Conditional Download (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Limited-download-browser-js-sdk"
---

When downloading a file (Object), you can specify one or more constraints. If the specified conditions are met, the download will proceed; if the conditions are not met, an error will be returned and the download process will not be initiated.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent the exposure of your BytePlus account credentials (namely, AccessKey ID and AccessKey Secret) in a browser environment, it is strongly recommended to perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access BytePlus TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* Endpoint is the access domain name for TOS external services. For information about endpoints supported by TOS, please refer to [Access Domain Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before downloading an object, you must have the `tos:GetObject` permission. For more information, see the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For more information, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object many times simultaneously, your access speed will be limited by TOS bandwidth and regional restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. For more information on accessing TOS through CDN, see [Accelerating Access to TOS Resources Using CDN](https://docs.byteplus.com/docs/6349/106079).

* Different conditions can be combined; for example, both If\-Modified\-Since and If\-Unmodified\-Since may be present simultaneously, and both If\-Match and If\-None\-Match may also coexist.

* Supports using the **headObject** interface of the TOS Browser SDK to retrieve the Etag information of an object.


<span id=".6ZmQ5a6a5p2h5Lu26K-05piO"></span>
## Explanation of Limiting Conditions

When downloading an object, you can specify conditions for the download. The object will be downloaded only when these conditions are met. The limiting conditions are as follows:


|Parameter |Description |
|---|---|
|If\-Match |The object is returned only if it has a matching ETag; otherwise, 412 Precondition Failed is returned. |
|If\-None\-Match |The object is returned only if it has a different ETag; otherwise, 304 Not Modified is returned. |
|If\-Modified\-Since |The object is returned only if it has been modified since the specified time; otherwise, 304 Not Modified is returned. |
|If\-Unmodified\-Since |The object is returned only if it has not been modified since the specified time; otherwise, `412 Precondition Failed` is returned. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following sample code is used to download files under specified conditions.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <button id="upload">Upload</button>
    <button id="download">Download</button>
    <input id="file" type="file" />
    <script src="https://tos-public.volccdn.com/obj/volc-tos-public/@volcengine/tos-sdk@latest/browser/tos.umd.production.min.js"></script>
    <script type="text/javascript">
      const client = new TOS({
        region: yourRegion,
        endpoint: yourEndpoint,
        accessKeyId: yourAccessKey,
        accessKeySecret: yourSecretKey,
        stsToken: yourSecurityToken,
        bucket: examplebucket,
      });
      const name = 'exampledir/getobjectv2.txt';
      let targetObjectETag = '';

      const upload = document.getElementById('upload');
      upload.addEventListener('click', async () => {
        const data = document.getElementById('file').files[0];

        try {
          const partSize = 5 * 1024 * 1024;

          await client.uploadFile({
            key: name,
            file: data,
            partSize,
          });

          const result = await client.headObject({ key: name });
          targetObjectETag = result.headers.etag;
          console.log('targetObjectETag', targetObjectETag);
        } catch (e) {
          console.log(e);
        }
      });

      const download = document.getElementById('download');
      download.addEventListener('click', async () => {
        try {
          const result = await client.getObjectV2({
            key: name,
            ifMatch: targetObjectETag,
            dataType: 'blob',
          });
          const blob = result.data.content;
          const link = document.createElement('a');
          link.href = window.URL.createObjectURL(blob);
          link.download = 'getobjectv2.txt';
          link.click();
          window.URL.revokeObjectURL(link.href);
        } catch (e) {
          console.log(e);
        }
      });
    </script>
  </body>
</html>
```
