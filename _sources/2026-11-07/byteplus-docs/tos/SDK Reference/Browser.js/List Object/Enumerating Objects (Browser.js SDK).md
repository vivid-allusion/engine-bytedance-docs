---
title: "Enumerating Objects (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-browser-js-sdk"
---

This article describes how to list objects within a specified bucket and objects with a specified prefix, with a default maximum return of 1,000 objects.

<span id=".5Yqf6IO96K-05piO"></span>
## Feature description

You can use listObjects to enumerate object information within a bucket, with a maximum of 1,000 objects returned per request. When using listObjects to list objects, owner information is returned by default. The parameters are described below:


|**Parameter** |**Description** |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |A character used to group object names. |
|marker |The starting point of the objects enumerated in this instance. |
|encodingType |Returns the key encoding type. |
|maxKeys |Maximum return count. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent exposure of your BytePlus account credentials (namely, AccessKey ID and AccessKey Secret) in browser environments, it is strongly recommended that you perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access BytePlus TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* The Endpoint is the access domain name for TOS external services. For information on endpoints supported by TOS, please refer to [Endpoint Domain](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### Brief Enumeration

The following code is used to list 10 objects in the specified bucket.

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

      client
        .listObjects({
          maxKeys: 10,
        })
        .then(data => {
          console.log(`listObjects bucketName:${examplebucket} data: `, data);
        });
    </script>
  </body>
</html>
```


<span id=".5YiG6aG15YiX5Li-"></span>
### Paginated Listing

The following code is used to list objects in the specified bucket with pagination.

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
        const { data } = await client.listObjects({
          maxKeys: 10,
        });
        console.log('firstPage', data);

        const secondPage = await client.listObjects({
          bucket: examplebucket,
          maxKeys: 10,
          marker: data.NextMarker,
        });
        console.log('secondPage', secondPage.data);
      };

      listObjects();
    </script>
  </body>
</html>
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### List all objects with the specified prefix

The following code is used to list all objects in the bucket with the specified prefix.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>

  <body>
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
        const data = await client.listObjects({
          bucket: examplebucket,
          maxKeys: 10,
          prefix: '10',
        });
        console.log('data', data.data);
      };

      listObjects();
    </script>
  </body>
</html>
```


<span id=".5YiX5Li-5qG25YaF5omA5pyJ5a-56LGh"></span>
### List all objects in the bucket

The following code enumerates all objects within the specified storage bucket.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Document</title>
</head>

<body>
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

      const data = await client.listObjects({
        bucket: examplebucket,
      });
      console.log('data', data.data);
    };

    listObjects();
  </script>
</body>
</html>
```


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
### List files and subdirectories in the specified directory

TOS recognizes only the concept of objects; it is possible to create an object with a size of zero and a slash.`/`The object at the end simulates the functionality of a directory. The functionality of a directory can be simulated using the `delimiter` and `prefix` parameters:


* First, set `delimiter` to`/`At the same time, when `prefix` is set to empty, objects and subdirectory information in the root directory can be returned.

* When setting `delimiter` to`/`Additionally, setting `prefix` as a subdirectory (subfiledir) allows you to return objects and subdirectories within it.


The following code is used to list the objects and subdirectories within a specified directory of the bucket.

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
        const data = await client.listObjects({
          bucket: examplebucket,
          delimiter: 'example_dir',
        });
        console.log('data', data.data);
      };

      listObjects();
    </script>
  </body>
</html>
```
