---
title: "List Unmerged Objects (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-unmerged-objects-browser-js-sdk"
---

This interface is used to list unmerged objects in a bucket, that is, to enumerate multipart upload tasks.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent your Volcengine account credentials (namely, AccessKey ID and AccessKey Secret) from being exposed in browser environments, it is strongly recommended that you perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access Volcengine TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* The Endpoint is the access domain name for TOS external services. For information on Endpoints supported by TOS, please refer to [Access Domain Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before listing multipart upload tasks, you must have the `tos:ListBucketMultipartUploads` permission. For more information, please refer to [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters


|Parameter |Description |
|---|---|
|delimiter |Character used to group object names. |
|encodingType |Encode the returned content and specify the type of encoding.<br><br>Default value: None |
|maxUploads |Returns the maximum number of multipart upload tasks. The default value is 1000.<br><br>Value range: (0, 1000] |
|prefix |Specifies to list in\-progress uploads only for those keys that begin with the specified prefix. |
|keyMarker |List the starting positions of multipart upload tasks. Objects are listed in alphabetical order after the specified start. This is typically the value of `nextMarker` returned by the previous request. |
|uploadIDMarker |Used in conjunction with `keyMarker`, this sets the return of the multipart upload task list to start from the value following the marker, sorted in lexicographical order. Obtain `nextVersionIdMarker` from the previous listing results. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### Brief Enumeration

The following code is used to list up to 10 unmerged multipart upload tasks in the specified storage bucket.

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

      const listMultipartUploads = async () => {
        const data = await client.listMultipartUploads({
          bucket: examplebucket,
          maxUploads: 10,
        });
        console.log('data', data.data);
      };

      listMultipartUploads();
    </script>
  </body>
</html>
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5pyq5ZCI5bm255qE5YiG54mH5Lu75Yqh"></span>
### List all unmerged shard tasks with the specified prefix

The following code enumerates all unmerged multipart upload tasks under the specified bucket and prefix.

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

      const listMultipartUploads = async () => {
        const data = await client.listMultipartUploads({
          bucket: examplebucket,
          prefix: '000',
        });
        console.log('data', data.data);
      };

      listMultipartUploads();
    </script>
  </body>
</html>
```


<span id=".5YiX5Li-5omA5pyJ5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### List all multipart upload tasks

The following code is used to list all unmerged multipart upload tasks for the specified bucket.

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

      const listMultipartUploads = async () => {
        const data = await client.listMultipartUploads({
          bucket: examplebucket,
        });
        console.log('data', data.data);
      };

      listMultipartUploads();
    </script>
  </body>
</html>
```
