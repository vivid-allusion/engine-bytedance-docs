---
title: "Listing Multi-Version Objects (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-multiversion-objects-browser-js-sdk"
---

This API is used to list multiversion objects in a bucket. This API returns a maximum of 1,000 multiversion objects in the bucket for each request. You can use request parameters to define the selection criteria for the objects to list.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent your Volcengine account credentials (namely, AccessKey ID and AccessKey Secret) from being exposed in browser environments, it is strongly recommended that you perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access Volcengine TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* Endpoint is the access domain name for TOS external services. For information on the Endpoints supported by TOS, please refer to [Endpoint for Access Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before listing versioned objects, you must have the `tos:ListBucket` permission. For more information, see [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters


|Parameter |Description |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |Character used to group object names. |
|maxKeys |Returns the maximum number of objects to be listed; the default value is 1000.<br><br>Value range: (0, 1000] |
|encodingType |Encode the returned content and specify the encoding type.<br><br>Default value: None |
|keyMarker |List the starting positions of multi\-version objects. Objects are listed in alphabetical order after the specified start. This is typically the value of `next_marker` returned by the previous request. |
|versionIdMarker |Used in conjunction with `KeyMarker`, this sets the operation to return the list of version objects sorted lexicographically starting after the specified value. Obtain `VersionIdMarker` from the previous listing results. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### A brief enumeration

The following code is used to list up to 10 multi\-version objects in the specified storage bucket.

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

      const listObjects = async () => {
        const data = await client.listObjectVersions({
          bucket: examplebucket,
          maxKeys: 10,
        });
        console.log('data', data.data);
      };

      listObjects();
    </script>
  </body>
</html>
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### List all objects with the specified prefix

The following code is used to enumerate all versioned objects and delete markers under the specified prefix in the designated storage bucket.

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

      const listObjects = async () => {
        const data = await client.listObjectVersions({
          bucket: examplebucket,
          prefix: '1',
        });
        console.log('data', data.data);
      };

      listObjects();
    </script>
  </body>
</html>
```


<span id=".5YiX5Li-5omA5pyJ5a-56LGh"></span>
### List all objects

The following code is used to enumerate all multi\-version objects and delete markers within the specified bucket.

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

      const listObjects = async () => {
        const data = await client.listObjectVersions({
          bucket: examplebucket,
        });
        console.log('data', data.data);
      };

      listObjects();
    </script>
  </body>
</html>
```
