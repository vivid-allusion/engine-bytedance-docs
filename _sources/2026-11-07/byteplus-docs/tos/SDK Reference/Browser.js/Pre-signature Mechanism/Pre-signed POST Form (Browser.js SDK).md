---
title: "Pre-signed POST Form (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Post-form-pre-signature-browser-js-sdk"
---

This article provides example code for presigned POST forms.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used for using a presigned POST form to bucket. When adding the object `preSignedUrl-put.txt` to `examplebucket`, generate the corresponding POST form signature data.

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
        const result = await client.preSignedPostSignature({
          bucket: examplebucket,
          key: objectName,
        });
        console.log('preSignedPostSignature:', result);
      };

      main();
    </script>
  </body>
</html>
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For detailed information about presigned POST forms, see [Forms for browser-based uploads that contain a signature](https://docs.byteplus.com/docs/tos/reference-browser-based-upload-forms-include-signatures).
