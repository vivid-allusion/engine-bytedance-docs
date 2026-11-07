---
title: "Resumable Upload (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume-upload-browser-js-sdk"
---

When uploading files to TOS using the resumable upload method, you can configure parameters such as part size, upload concurrency, and event callback functions. During the upload process, if a network error or program crash results in a failed file upload, the system will resume uploading the incomplete portion from the last recorded breakpoint. During the upload process, you can cancel the object upload by invoking the Cancel method of the passed\-in cancelToken.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent exposure of your BytePlus account credentials (namely, AccessKey ID and AccessKey Secret) in browser environments, it is strongly recommended that you perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access BytePlus TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* Endpoint is the domain name used to access TOS external services. For information on endpoints supported by TOS, please refer to [Access Domain Name Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before uploading an object, you must have the `tos:PutObject` permission. For specific instructions, refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading objects, object names must comply with specific conventions. For more information, see [Object Naming Conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale data storage, with internal partitions storing object index data. To maximize throughput scalability when uploading and downloading objects and to reduce the likelihood of hotspot partitions, please avoid using lexicographically incremental object naming. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.

* The SDK records the upload status information in the `Checkpoint` file, so the program must have write permissions for the `Checkpoint` file.

* When using resumable upload, the progress information of the file upload is recorded in the `Checkpoint` file. If a part of the upload fails during the process, when uploading again, it will continue from the point recorded in the `Checkpoint` file. After the upload is complete, the `Checkpoint` file will be deleted.

* If the local file is modified during the upload process, all segments will be re\-uploaded.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5LiK5Lyg5paH5Lu2"></span>
### Object upload

The following code is used to upload files using the resumable upload method.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <button id="upload">Upload</button>
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

      const upload = document.getElementById('upload');
      upload.addEventListener('click', async () => {
        const data = document.getElementById('file').files[0];
        console.log('data', data);

        try {
          const partSize = 5 * 1024 * 1024;

          const result = await client.uploadFile({
            key: 'exampledir/putObjectobject.txt',
            file: data,
            partSize,
            taskNum: 5,
            progress: (p, cpt) => {
              abortCheckpoint = cpt;
              console.log(p * 100);
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


<span id=".5Y-W5raI57ut5Lyg5py65Yi2"></span>
### Cancellation of the Resumable Transfer Mechanism

The following code is used to cancel an active resumable upload task during runtime.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <button id="upload">Upload</button>
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

      const upload = document.getElementById('upload');
      upload.addEventListener('click', async () => {
        const data = document.getElementById('file').files[0];
        console.log('data', data);

        const partSize = 5 * 1024 * 1024;

        let cancelTokenSource = TOS.CancelToken.source();
        let tosCheckpoint;

        client.uploadFile({
          key: 'exampledir/canclePutObjectobject.txt',
          file: data,
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
          client.uploadFile({
            key: 'exampledir/canclePutObjectobject.txt',
            file: data,
            partSize,
            checkpoint: tosCheckpoint,
            cancelToken: cancelTokenSource.token,
            progress: (percent, checkpoint) => {
              tosCheckpoint = checkpoint;
              console.log(percent, checkpoint);
            },
          });
        }, 5000);
      });
    </script>
  </body>
</html>
```
