---
title: "Range Download (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Scope-download-browser-js-sdk"
---

If you only need to retrieve a portion of the data within an object, you can use range download to obtain data within a specified range. This article explains how to perform range download.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent your Volcengine account credentials (namely, AccessKey ID and AccessKey Secret) from being exposed in browser environments, it is strongly recommended that you perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access Volcengine TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* The Endpoint is the access domain name used by TOS for external services. For information on endpoints supported by TOS, please refer to [Access Domain Name Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before downloading an object, you must have the `tos:GetObject` permission. For more information, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For more information, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object many times simultaneously, your access speed will be limited by TOS bandwidth and regional restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. For more information on accessing TOS through CDN, see [Accelerating Access to TOS Resources Using CDN](https://docs.byteplus.com/docs/6349/106079).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to specify a Range for downloading partial data from an object in the bucket.

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
      const name = 'exampledir/range.txt';

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
        } catch (e) {
          console.log(e);
        }
      });

      const download = document.getElementById('download');
      download.addEventListener('click', async () => {
        try {
          const result = await client.getObjectV2({
            key: name,
            dataType: 'blob',
            headers: { Range: 'bytes=0-9' },
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
