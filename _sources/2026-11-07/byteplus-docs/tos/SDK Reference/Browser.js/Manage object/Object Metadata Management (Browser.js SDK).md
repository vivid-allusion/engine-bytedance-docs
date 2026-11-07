---
title: "Object Metadata Management (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-meta-information-browser-js-sdk"
---

Object metadata refers to the description of an object's properties, which includes both HTTP standard attributes (HTTP Header) and user\-defined metadata (User Meta).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* To prevent the exposure of your Volcengine account credentials (namely, AccessKey ID and AccessKey Secret) in browser environments, it is strongly recommended that you perform TOS\-related operations using temporary access credentials. For detailed instructions, please refer to [Using STS Temporary AK/SK+Token to Access Volcengine TOS](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service).

* The Endpoint is the access domain name for TOS's external services. For information about Endpoints supported by TOS, please refer to [Access Domain Name Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Only the object owner has permission to set object metadata.

* When setting user\-defined metadata, the Key must consist only of lowercase English letters and cannot contain spaces or other special characters.


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

The TOS Browser SDK enables users to add and modify metadata for objects that have already been uploaded. TOS supports carrying the following request headers to modify object metadata. When downloading an object or performing a HEAD request, these values are set in the HTTP header and returned to the client. The request headers are as follows:


|  |Description |
|---|---|
|Content\-Type |Object content type, |
|Cache\-Control |Specifies the caching behavior when the object is downloaded. |
|Expires |Specifies the cache expiration time as defined in RFC 2616. |
|Content\-Disposition |Specifies the default filename of the object when downloaded. |
|Content\-Encoding |Specifies the content encoding of the object when downloaded. |
|Content\-Language |Specifies the content language of the object when downloaded. |
|x\-tos\-meta\-\* |Metadata information set when setting the `Meta` field using the SDK. When this object is queried, the metadata will be included in the Header of the returned message. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5pmu6YCa5LiK5Lyg5pe26K6-572u5YWD5pWw5o2u5L-h5oGv"></span>
### Configuring Metadata Information During Standard Upload

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
      const objectName = 'exampledir/putObjectobject.txt';

      const upload = document.getElementById('upload');
      upload.addEventListener('click', async () => {
        const data = document.getElementById('file').files[0];
        console.log('data', data);

        try {
          const result = await client.uploadFile({
            key: objectName,
            file: data,
            headers: {
              'content-type': 'text/plain',
              expires: new Date('2028/01/01'),
            },
          });
          console.log(result);

          const headobject = await client.headObject({
            bucket: examplebucket,
            key: objectName,
          });
          // object info
          console.log('object info:', headobject.data);
        } catch (e) {
          console.log(e);
        }
      });
    </script>
  </body>
</html>
```


<span id=".6YCa6L-HLXNldG9iamVjdG1ldGEt6K6-572u5a-56LGh5YWD5pWw5o2u5L-h5oGv"></span>
### Set object metadata information using SetObjectMeta.

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
        bucket: bucketName,
      });
      const objectName = 'exampledir/putObjectobject.txt';

      const main = async () => {
        const { data } = await client.headObject({
          bucket: bucketName,
          key: objectName,
        });
        console.log('object info:', data);
        console.log('object content-type:', data['content-type']);
        console.log('object expires:', data.expires);

        await client.setObjectMeta({
          bucket: bucketName,
          key: objectName,
          headers: {
            'Content-Language': 'zh-cn',
            'Content-Type': 'text/html',
            Expires: new Date('2030'),
          },
        });

        const { data: newData } = await client.headObject({
          bucket: bucketName,
          key: objectName,
        });
        console.log('object info:', newData);
        console.log('object content-type:', newData['content-type']);
        console.log('object expires:', newData.expires);
        console.log('object content-language:', newData['content-language']);
      };

      main();
    </script>
  </body>
</html>
```


<span id=".5p-l6K-i5a-56LGh5YWD5pWw5o2u5L-h5oGv77yI5Yik5pat5a-56LGh5piv5ZCm5a2Y5Zyo77yJ"></span>
### Query Object Metadata (Determine Whether the Object Exists)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before obtaining object metadata, you must have the <code>tos:GetObject</code> permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-overview_6">IAM Policy Overview</a>.</div>


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
        bucket: bucketName,
      });
      const objectName = 'exampledir/putObjectobject.txt';

      const main = async () => {
        const { data } = await client.headObject({
          bucket: bucketName,
          key: objectName,
        });
        console.log('object info:', data);
      };

      main();
    </script>
  </body>
</html>
```
