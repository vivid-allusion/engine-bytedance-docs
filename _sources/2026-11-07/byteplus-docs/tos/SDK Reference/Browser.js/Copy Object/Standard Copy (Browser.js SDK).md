---
title: "Standard Copy (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-copy-browser-js-sdk"
---

The copyObject operation enables copying objects between buckets within the same region, as well as copying objects within a single bucket. During copying, you can specify new metadata information or retain the metadata of the source object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent the exposure of your Volcengine account credentials (namely, AccessKey ID and AccessKey Secret) in browser environments, it is strongly recommended that you perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access Volcengine TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* The Endpoint is the access domain name for TOS external services. For information on Endpoints supported by TOS, please refer to [Endpoint for Access Domain Names](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Object copying does not support cross\-region bucket\-to\-bucket copying.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can retain all metadata (by default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to use copyObject to copy the object srcObject from the bucket srcBucket to the object dstObject in the bucket dstBucket.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <button id="upload">Upload</button>
    <button id="copy">Copy</button>
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

      const srcBucket = srcBucket; 
      const srcKey = 'exampledir/putObject-test'; 
      const dstBucket = dstBucket; 
      const dstObject = 'exampledir/copy-test'; 

      const upload = document.getElementById('upload');
      upload.addEventListener('click', async () => {
        const data = document.getElementById('file').files[0];
        try {
          await client.uploadFile({
            bucket: srcBucket,
            key: srcKey,
            file: data,
          });
        } catch (e) {
          console.log(e);
        }
      });

      const copy = document.getElementById('copy');
      copy.addEventListener('click', async () => {
        try {
          const result = await client.copyObject({
            bucket: dstBucket,
            key: dstObject,
            srcBucket,
            srcKey,
          });
          console.log('result', result);
        } catch (e) {
          console.log(e);
        }
      });
    </script>
  </body>
</html>
```
