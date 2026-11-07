---
title: "Incremental Upload (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-browser-js-sdk"
---

The AppendObjectV2 interface is used to perform append\-write operations on objects. Append write refers to adding content to the end of an already uploaded object. This interface can only be used with objects of type Appendable. Objects created through direct upload or multipart upload are of type Normal.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To avoid exposing your Volcengine account credentials (namely, AccessKey ID and AccessKey Secret) in a browser environment, it is strongly recommended that you perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access Volcengine TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* The Endpoint is the access domain name for TOS's external services. For information on the Endpoints supported by TOS, please refer to [Access Domain Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before you can append objects, you must have the `tos:PutObject` permission. For more information, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading objects, object names must comply with specific standards. For detailed information, see [Object Naming Standards](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for massive storage. Its internal partitions store object index data. To maximize the throughput of object uploads and downloads during horizontal scaling and to reduce the probability of hotspot partitions, please avoid using lexicographically incremental object naming. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. When multi\-versioning is enabled for a bucket, the original object is retained, and a new version number is generated to identify the newly uploaded object.


<span id=".6ZmQ5Yi26K-05piO"></span>
## Limitations

AppendObject has the following restrictions:


* The size of the object after appending must not exceed 5 GiB.

* When a PutObject operation is performed on an object created using AppendObject, the object is overwritten and its type changes from Appendable to Normal. Conversely, objects uploaded through PutObject cannot be appended with additional data.

* Objects created through AppendObject cannot be copied.

* If an object is in Infrequent Access Storage or Flashback Archive, data cannot be appended using AppendObject.

* If your bucket is in either the enabled or suspended state for multi\-versioning, the AppendObject interface cannot be used.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to perform append upload on objects.

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

      const upload = document.getElementById("upload");
      upload.addEventListene r("click", async () => {
        const data = document.getElementById("file").files[0];
        console.log("data", data);

        await client.appendObject({
          key: "exampledir/exampleobject.txt",
          body: data,
          offset: 0,
        });
      });
    </script>
  </body>
</html>
```
