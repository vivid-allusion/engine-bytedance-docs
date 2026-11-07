---
title: "Standard Presigned URL (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-pre-signature-node-js-sdk"
---

By default, TosClient includes a signature in the request header when initiating a request to the server. The SDK also supports generating signed URLs, which can be used directly to initiate HTTP requests or shared with third parties to enable access authorization.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIrkvKDlr7nosaE="></span>
### Uploading Objects Using Pre\-Signed URLs

The following code is used to upload objects to a specified bucket via a pre\-signed URL.

```javascript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
import axios from 'axios';

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
    const url = client.getPreSignedUrl({
      method: 'PUT',
      bucket: bucketName,
      key: objectName,
    });
    console.log('PreSignedUrl:', url);

    const uploadResult = await axios.put(url, 'hello world from PreSignedUrl');

    const { data } = await client.headObject({
      bucket: bucketName,
      key: objectName,
    });
    console.log('object size:', data['content-length']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIvovb3lr7nosaE="></span>
### Downloading Objects Using Pre\-Signed URLs

The following code is used to download an object from the specified bucket using a pre\-signed URL.

```javascript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

import axios from 'axios';

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
    const url = client.getPreSignedUrl({
      method: 'GET',
      bucket: bucketName,
      key: objectName,
    });
    console.log('PreSignedUrl:', url);

    const result = await axios.get(url);
    console.log('get result:', result.data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3liKDpmaTlr7nosaE="></span>
### Deleting Objects Using Pre\-Signed URLs

The following code is used to delete objects in a specified bucket via a pre\-signed URL.

```javascript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

import axios from 'axios';

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
    const url = client.getPreSignedUrl({
      method: 'DELETE',
      bucket: bucketName,
      key: objectName,
    });
    console.log('PreSignedUrl:', url);

    const result = await axios.delete(url);
    console.log('delete result:', result);
  } catch (error) {
    handleError(error);
  }
}

main();
```
