---
title: "Chunked Copy (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-copy-browser-js-sdk"
---

When an object exceeds 5 GiB in size, multipart copy is required.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent the exposure of your BytePlus account credentials (namely, AccessKey ID and AccessKey Secret) in browser environments, it is strongly recommended that you perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access BytePlus TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* Endpoint is the access domain name for TOS external services. For information on endpoints supported by TOS, please refer to [Access Domain Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Object copy does not support cross\-region bucket\-to\-bucket copying.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you may retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".5YiG54mH5ou36LSd5q2l6aqk"></span>
## Shard Copy Procedure


1. Initialize the multipart copy task using createMultipartUpload.

2. Multipart copy is performed using uploadPartCopy.

3. Merge parts using completeMultipartUpload.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used for multipart copying of objects.

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

      const srcBucket = yourSrcBucket; 
      const srcObject = 'exampledir/putObject-test'; 
      const dstBucket = yourDstBucket; 
      const dstObject = 'exampledir/part-copy-test'; 

      const upload = document.getElementById('upload');
      upload.addEventListener('click', async () => {
        const data = document.getElementById('file').files[0];
        try {
          await client.uploadFile({
            bucket: srcBucket,
            key: srcObject,
            file: data,
          });
        } catch (e) {
          console.log(e);
        }
      });

      const copy = document.getElementById('copy');
      copy.addEventListener('click', async () => {
        try {
          const {
            data: { UploadId },
          } = await client.createMultipartUpload({
            bucket: dstBucket,
            key: dstObject,
          });
          console.log('UploadId', UploadId);

          const {
            data: { 'content-length': contentLength },
          } = await client.headObject({
            bucket: srcBucket,
            key: srcObject,
          });
          console.log('srcObject content-length', contentLength);

          const totalSize = contentLength;
          const partSize = 5 * 1024 * 1024;

          let offset = 0;
          let partNumber = 1;
          const partsInfo = [];

          while (offset < totalSize) {
            const uploadResult = await client.uploadPartCopy({
              bucket: dstBucket,
              key: dstObject,
              partNumber,
              uploadId: UploadId,
              headers: {
                'x-tos-copy-source': `/${srcBucket}/${srcObject}`,
                'x-tos-copy-source-range': `bytes=${offset}-${offset + partSize}`,
              },
            });
            const eTag = uploadResult.data.ETag;
            console.log(`partNumber${partNumber} Etag:`, eTag);
            partsInfo.push({
              partNumber,
              eTag,
            });
            partNumber++;
            offset += partSize;
          }
          console.log('parts information', partsInfo);

          const { data } = await client.completeMultipartUpload({
            bucket: dstBucket,
            key: dstObject,
            uploadId: UploadId,
            parts: partsInfo,
          });

          console.log('result data:', data);
        } catch (e) {
          console.log(e);
        }
      });
    </script>
  </body>
</html>
```
