---
title: "Standard Upload (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-upload-browser-js-sdk"
---

When the file you upload is smaller than 5 GiB, you can use the simple upload method (that is, the PutObject method) to upload files or data to TOS.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent exposure of your Volcengine account credentials (namely, AccessKey ID and AccessKey Secret) in browser environments, it is strongly recommended to perform TOS operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access Volcengine TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* Endpoint is the access domain name for TOS external services. For information on endpoints supported by TOS, please refer to [Access Domain Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before uploading an object, you must have the `tos:PutObject` permission. For more information, see the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading objects, object names must comply with specific standards. For detailed information, please refer to [Object Naming Guidelines](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale data storage, with internal partitions that store object index data. To maximize the throughput when uploading and downloading objects and to reduce the likelihood of hot partitions, please avoid using object names that increase in lexicographical order. For more details, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. If versioning is enabled for your bucket, the original object will be retained, and a new version number will be generated to identify the newly uploaded object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to upload data to the file exampleobject.txt located in the exampledir directory of examplebucket.

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

      const headers = {
      };

      async function putObject(data) {
        try {
          const result = await client.putObject({
            key: "exampledir/exampleobject.txt",
            body: data,
          });
          console.log(result);
        } catch (e) {
          console.log(e);
        }
      }

      const upload = document.getElementById("upload");
      upload.addEventListener("click", () => {
        const data = document.getElementById("file").files[0];
        console.log("data", data);

        putObject(data);
      });
    </script>
  </body>
</html>
```
