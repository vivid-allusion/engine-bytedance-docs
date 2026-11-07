---
title: "Standard Presigned Signature (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-pre-signature-browser-js-sdk"
---

By default, TosClient includes a signature in the request header when initiating requests to the server. The SDK also supports generating signed URLs, which users can use to initiate HTTP requests directly or share with third parties to grant access authorization.

<span id=".6aKE562-5ZCN6K-05piO"></span>
## Presigned Overview

By default, TosClient includes a signature in the request header when initiating a request to the server. The SDK also supports generating signed URLs, which can be used to initiate HTTP requests directly or shared with third parties to enable access authorization.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIrkvKDlr7nosaE="></span>
### Uploading Objects Using Pre\-Signed URLs

The following code is used to upload objects to a specified bucket via a pre\-signed URL.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <script src="https://tos-public.volccdn.com/obj/volc-tos-public/@volcengine/tos-sdk@latest/browser/tos.umd.production.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/axios/1.4.0/axios.min.js"></script>
    <script type="text/javascript">
      const client = new TOS({
        region: yourRegion,
        endpoint: yourEndpoint,
        accessKeyId: yourAccessKey,
        accessKeySecret: yourSecretKey,
        stsToken: yourSecurityToken,
        bucket: examplebucket,
      });
      const objectName = 'exampledir/preSignedUrl-put.txt';

      const main = async () => {
        const url = client.getPreSignedUrl({
          method: 'PUT',
          bucket: examplebucket,
          key: objectName,
        });
        console.log('PreSignedUrl:', url);

        const uploadResult = await axios.put(url, 'hello world from PreSignedUrl');

        const { data } = await client.headObject({
          bucket: examplebucket,
          key: objectName,
        });

        console.log('object size:', data, data['content-length']);
      };

      main();
    </script>
  </body>
</html>
```


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIvovb3lr7nosaE="></span>
### Downloading Objects Using Pre\-Signed URLs

The following code is used to download objects from a specified bucket using a pre\-signed URL.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <script src="https://tos-public.volccdn.com/obj/volc-tos-public/@volcengine/tos-sdk@latest/browser/tos.umd.production.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/axios/1.4.0/axios.min.js"></script>
    <script type="text/javascript">
      const client = new TOS({
        region: yourRegion,
        endpoint: yourEndpoint,
        accessKeyId: yourAccessKey,
        accessKeySecret: yourSecretKey,
        stsToken: yourSecurityToken,
        bucket: examplebucket,
      });
      const objectName = 'exampledir/preSignedUrl-put.txt';

      const main = async () => {
        const url = client.getPreSignedUrl({
          method: 'GET',
          bucket: examplebucket,
          key: objectName,
        });
        console.log('PreSignedUrl:', url);

        const result = await axios.get(url);
        console.log('get result:', result.data);
      };

      main();
    </script>
  </body>
</html>
```


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3liKDpmaTlr7nosaE="></span>
### Deleting Objects Using Pre\-Signed URLs

The following code is used to delete objects in a specified bucket via a pre\-signed URL.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <script src="https://tos-public.volccdn.com/obj/volc-tos-public/@volcengine/tos-sdk@latest/browser/tos.umd.production.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/axios/1.4.0/axios.min.js"></script>
    <script type="text/javascript">
      const client = new TOS({
        region: yourRegion,
        endpoint: yourEndpoint,
        accessKeyId: yourAccessKey,
        accessKeySecret: yourSecretKey,
        stsToken: yourSecurityToken,
        bucket: examplebucket,
      });
      const objectName = 'exampledir/preSignedUrl-put.txt';

      const main = async () => {
        const url = client.getPreSignedUrl({
          method: 'DELETE',
          bucket: examplebucket,
          key: objectName,
        });
        console.log('PreSignedUrl:', url);

        const result = await axios.delete(url);
        console.log('delete result:', result);
      };

      main();
    </script>
  </body>
</html>
```
