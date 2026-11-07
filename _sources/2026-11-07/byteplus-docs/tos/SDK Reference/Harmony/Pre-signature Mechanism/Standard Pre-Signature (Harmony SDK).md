---
title: "Standard Pre-Signature (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-pre-signature-harmony-sdk"
---

By default, TosClient includes a signature in the request header when initiating a request to the server. The SDK also supports generating signed URLs, which can be used to initiate HTTP requests directly or shared with third parties to grant access authorization.

<span id="8a0bd5a3"></span>
## Generate a pre\-signed URL for uploading objects

The following code demonstrates how to generate a pre\-signed URL for uploading an object.

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
    const objectName =  'harmonyos-sdk-test-object';
    const res = await client.preSignedURL({
      Bucket: bucketName,
      Key:  objectName,
    })
    console.log('PreSignedUrl:', res.SignedUrl);
    await axios.put<string, AxiosResponse<string, Any>>(res.SignedUrl, 'put-content');
    const res2 = await client.headObject({
      Bucket: bucketName,
      Key: objectName,
    });
    console.log('date length: ', res2.ContentLength)

  } catch (error) {
    handleError(error);
  }
}
main();
```


<span id="576e4968"></span>
## Generate a pre\-signed URL for downloading objects

The following code demonstrates how to generate a presigned URL for downloading an object.

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
    const objectName =  'harmonyos-sdk-test-object';
    const res = await client.preSignedURL({
      Bucket: bucketName,
      Key:  objectName,
      HttpMethod: 'GET',
    })
    console.log('PreSignedUrl:', res.SignedUrl);
    const res2 = await axios.get<string, AxiosResponse<string, Any>>(res.SignedUrl);
    console.log('date length: ', res2.data)

  } catch (error) {
    handleError(error);
  }
}
main();
```
