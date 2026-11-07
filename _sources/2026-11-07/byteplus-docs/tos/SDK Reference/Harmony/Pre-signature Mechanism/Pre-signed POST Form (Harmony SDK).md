---
title: "Pre-signed POST Form (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Post-form-pre-signature-harmony-sdk"
---

This article provides example code for pre\-signed POST forms.

<span id="c2ee6e6b"></span>
## Sample Code

The following code is used to generate the POST form signature data required for adding the `putObject-from-preSignedPostSignature-test` object to the `node-sdk-test-bucket` bucket using a pre\-signed POST form.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your sk",
  securityToken: 'Provide your securityToken',
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
    const bucketName = 'harmonyos-sdk-test-bucket';
    const objectName = 'putObject-from-preSignedPostSignature-test';

    const res = await client.preSignedPostSignature({
      Bucket: bucketName,
      Key: objectName,
      Expires: 3600,
    });
    
    console.log('preSignedPostSignature:', res.Signature);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="c4cb3d4b"></span>
## Relevant Documentation

For detailed information on POST form presigning, see [Including signatures in browser-based upload forms](https://docs.byteplus.com/docs/tos/reference-browser-based-upload-forms-include-signatures).
