---
title: "Resumable Copy (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume-copy-browser-js-sdk"
---

The resumable copy process divides the object to be copied into multiple segments and supports concurrent copying. Once all segments have been copied, they are merged into a complete file.

<span id=".5pat54K557ut5Lyg5ou36LSd6K-05piO"></span>
## Resumable copy instructions

Resumable copy is suitable for scenarios where large objects are copied using the TOS Browser SDK, either within a single bucket or between two buckets in the same region. The TOS Browser SDK provides resumable copy functionality. It uses a local checkpoint mechanism to record successfully copied segments. If segment copying is interrupted due to network issues or hardware failures, you can call the interface again to resume the transfer. You can configure the segment size for resumable copy operations, the concurrency level for segment copying, event callback functions, and other related parameters. It is also possible to cancel the task during the execution of the resumable copy operation.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent the exposure of your account credentials (namely, AccessKey ID and AccessKey Secret) in browser environments, it is strongly recommended that you perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS temporary AK/SK+token to access TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* The Endpoint is the access domain name for TOS external services. For information on Endpoints supported by TOS, please refer to [Endpoints](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Object copying does not support cross\-region bucket\-to\-bucket copying.

* When copying an object, the account must have read permission on the source object and write permission on the destination bucket.

* When copying an object, you can retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code enables resumable copying of the srcObject object from the srcBucket to the dstBucket, sets the object name to dstObject, and resumes the copy after a failure. If a network timeout error occurs during the copy process, invoke **resumableCopyObject** with the same parameters to resume the interrupted copy from the breakpoint.

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
      const srcObject = 'exampledir/putResumableObject-test'; 
      const dstBucket = yourDstBucket; 
      const dstObject = 'exampledir/resumableCopyObject-test'; 
      const partSize = 5 * 1024 * 1024; 

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

      let cancelTokenSource = TOS.CancelToken.source();
      let tosCheckpoint;

      const copy = document.getElementById('copy');
      copy.addEventListener('click', async () => {
        try {
          client.resumableCopyObject({
            bucket: dstBucket,
            key: dstObject,
            srcBucket,
            srcKey: srcObject,
            partSize,
            cancelToken: cancelTokenSource.token,
            progress: (percent, checkpoint) => {
              tosCheckpoint = checkpoint;
              console.log(percent, checkpoint);
            },
          });

          setTimeout(() => {
            cancelTokenSource.cancel('manual cancel');
            console.log('cancel request');
          }, 1000);

          setTimeout(() => {
            cancelTokenSource = TOS.CancelToken.source();
            client.resumableCopyObject({
              bucket: dstBucket,
              key: dstObject,
              srcBucket,
              srcKey: srcObject,
              partSize,
              checkpoint: tosCheckpoint,
              cancelToken: cancelTokenSource.token,
              progress: (percent, checkpoint) => {
                tosCheckpoint = checkpoint;
                console.log(percent, checkpoint);
              },
            });
          }, 5000);
        } catch (e) {
          console.log(e);
        }
      });
    </script>
  </body>
</html>
```
