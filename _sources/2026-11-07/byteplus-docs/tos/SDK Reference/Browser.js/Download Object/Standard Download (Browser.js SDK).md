---
title: "Standard Download (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-download-browser-js-sdk"
---

The GetObject method enables downloading objects from a specified bucket. Before using this interface, ensure that you have read access to the object. When using the download interface, you can obtain current download data progress information by configuring a progress bar callback.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent exposure of your Volcengine account credentials (namely, AccessKey ID and AccessKey Secret) in browser environments, it is strongly recommended to perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access Volcengine TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* The Endpoint is the access domain name for TOS external services. For information on endpoints supported by TOS, please refer to [Access Domain Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before downloading an object, you must have the `tos:GetObject` permission. For more information, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For more information, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object in large quantities simultaneously, your access speed will be subject to limitations imposed by TOS bandwidth and geographic restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. For more information on accessing TOS through CDN, see [Accelerating Access to TOS Resources Using CDN](https://docs.byteplus.com/docs/6349/106079).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following sample code is used to obtain the preview and download URL for the file exampleobject.txt in examplebucket.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <button id="upload">Upload</button>
    <button id="preview">Get the preview URL</button>
    <button id="download">Get the download URL</button>
    <input id="file" type="file" />
    <script src="https://tos-public.volccdn.com/obj/volc-tos-public/@volcengine/tos-sdk@latest/browser/tos.umd.production.min.js"></script>
    <script src="./const.js"></script>
    <script type="text/javascript">
      const client = new TOS({
        region: yourRegion,
        endpoint: yourEndpoint,
        accessKeyId: yourAccessKey,
        accessKeySecret: yourSecretKey,
        stsToken: yourSecurityToken,
        bucket: examplebucket,
      });
      const name = 'exampledir/exampleobject.txt';

      const upload = document.getElementById('upload');
      upload.addEventListener('click', async () => {
        const data = document.getElementById('file').files[0];
        console.log('data', data);

        try {
          const partSize = 5 * 1024 * 1024;

          const result = await client.uploadFile({
            key: name,
            file: data,
            partSize,
          });
          console.log(result);
        } catch (e) {
          console.log(e);
        }
      });

      const preview = document.getElementById('preview');
      preview.addEventListener('click', async () => {
        try {
          const result = await client.getPreSignedUrl({
            key: name,
            expires: 3600,
          });
          console.log(result);
        } catch (e) {
          console.log(e);
        }
      });

      const download = document.getElementById('download');
      download.addEventListener('click', async () => {
        try {
          const filename = 'examplefile.txt';
          const result = await client.getPreSignedUrl({
            key: name,
            expires: 3600,
            response: {
              contentDisposition: `attachment; filename=${filename}`,
            },
          });
          console.log(result);
        } catch (e) {
          console.log(e);
        }
      });
    </script>
  </body>
</html>
```
