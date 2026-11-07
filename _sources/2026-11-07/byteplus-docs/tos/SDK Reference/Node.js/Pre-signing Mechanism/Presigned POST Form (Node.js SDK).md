---
title: "Presigned POST Form (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Post-form-presignature-node-js-sdk"
---

This article provides sample code for pre\-signed POST forms.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to upload to the bucket using a pre\-signed POST form. When adding the object `putObject-from-PreSignedUrl-test` to `node-sdk-test-bucket`, the corresponding POST form signature data is generated.

```javascript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'], 
  accessKeySecret: process.env['TOS_SECRET_KEY'], 
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});

function handleError(error) {
  if (error instanceof TosClientError) {
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Header:', error.headers);
    console.log('Response Err Code:', error.code);
    console.log('Response Err Msg:', error.message);
  } else {
    console.log('unexpected exception, message: ', error);
  }
}

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    const objectName = 'putObject-from-PreSignedUrl-test';
    
    const res = await client.preSignedPostSignature({
      bucket: bucketName,
      key: objectName,
      expiresIn: 3600,
    });
    console.log('preSignedPostSignature:', res);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For detailed information on POST form presigning, see [Including a signature in browser-based upload forms](https://docs.byteplus.com/docs/tos/reference-browser-based-upload-forms-include-signatures).
