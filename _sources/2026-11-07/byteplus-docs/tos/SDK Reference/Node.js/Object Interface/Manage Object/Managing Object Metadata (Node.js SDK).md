---
title: "Managing Object Metadata (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-meta-information-node-js-sdk"
---

Object meta\-information is a description of an object's attributes, including HTTP headers and user\-defined metadata.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only the object owner has permission to set object metadata.

* When setting user\-defined metadata, the English alphabet custom metadata Key only supports lowercase, and does not support special characters such as spaces.


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

The TOS Node.js SDK allows you to add and modify metadata information for objects that have been uploaded. TOS supports modifying object metadata with the following 7 request headers. When downloading an object or HEAD object, these values are set in the HTTP header field and returned to the client side. The request header is as follows:


|name |explain |
|---|---|
|Content\-Type |Object type. |
|Cache\-Control |Specifies the caching behavior of web pages when the object is downloaded. |
|Expires |Cache expiration time as defined in RFC 2616. |
|Content\-Disposition |The name of the object when it was downloaded. |
|Content\-Encoding |The content encoding type of the object when it was downloaded. |
|Content\-Language |The content language format of the object when it was downloaded. |
|x\-tos\-meta\-\* |The metadata information set when setting a `meta`field using the SDK. When querying this object, the metadata will be in the header of the returned message. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5pmu6YCa5LiK5Lyg5pe26K6-572u5YWD5pWw5o2u5L-h5oGv"></span>
### Set metadata on normal upload

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
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

const bucketName = 'node-sdk-test-bucket';
// Upload the file to the example.txt file in the example_dir directory.
const objectKey = 'example_dir/example.txt';
async function main() {
  try {
    // Upload the string "Hello TOS" to the example.txt file in the specified example_dir directory.
    const body = Buffer.from('Hello TOS');
    const { requestId } = await client.putObject({
      bucket: bucketName,
      key: objectKey,
      body,
      // User-defined metadata information
      meta: {
        key: 'value',
      },
      // Set object type
      contentType: 'text/html',
      // Set content language format when downloading the object
      contentLanguage: 'zh-cn',
      // Set cache strategy
      cacheControl: 'no-store',
      // Set cache expiration time
      expires: new Date('2028/01/01'),
      // Set the name of the downloaded content
      contentDisposition: 'example.png',
      // Set encoding type when downloading
      contentEncoding: 'deflate',
    });
    console.log('putObject Request ID:', requestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="69a7462d"></span>
### **Shard upload settings metadata information**

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
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

const bucketName = 'node-sdk-test-bucket';
// Upload the file to the example.txt file under the example_dir directory.
const objectKey = 'example_dir/example.txt';
async function main() {
  try {
    // Upload the string "Hello TOS" to the example.txt file in the specified example_dir directory.
    const body = Buffer.from('Hello TOS');
    const { data, requestId } = await client.createMultipartUpload({
      bucket: bucketName,
      key: objectKey,
      body,
      // User-defined metadata information
      meta: {
        key: 'value',
      },
      // Set object type
      contentType: 'text/html',
      // Set content language format when downloading the object
      contentLanguage: 'zh-cn',
      // Set cache strategy
      cacheControl: 'no-store',
      // Set cache expiration time
      expires: new Date('2028/01/01'),
      // Set the name of the downloaded content
      contentDisposition: 'example.png',
      // Set encoding type when downloading
      contentEncoding: 'deflate',
    });
    const uploadId = data.UploadId;
    console.log('createMultipartUpload Request ID:', requestId);
    console.log('dcreateMultipartUpload UploadId:', uploadId);

    // Upload chunk data
    const { data: part, requestId: uploadPartRequestId } = await client.uploadPart({
      bucket: bucketName,
      key: objectKey,
      uploadId,
      partNumber: 1,
      body: Buffer.from('your body data'),
    });
    console.log('uploadPart Request ID:', uploadPartRequestId);

    // Complete upload.
    const { requestId: completeRequestId } = await client.completeMultipartUpload({
      bucket: bucketName,
      key: objectKey,
      uploadId,
      parts: [{ partNumber: 1, eTag: part.ETag }],
    });
    console.log('completeMultipartUpload Request ID:', completeRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6YCa6L-HLXNldG9iamVjdG1ldGEt6K6-572u5a-56LGh5YWD5pWw5o2u5L-h5oGv"></span>
### Set object metadata through SetObjectMeta

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
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

const bucketName = 'node-sdk-test-bucket';
// Object name in the storage bucket.
const objectKey = 'example_dir/example.txt';
async function main() {
  try {
    const { requestId } = await client.setObjectMeta({
      bucket: bucketName,
      key: objectKey,
      // User-defined metadata information
      meta: {
        key: 'value',
      },
      // Set object type
      contentType: 'text/html',
      // Set content language format when downloading object
      contentLanguage: 'zh-cn',
      // Set cache control strategy
      cacheControl: 'no-store',
      // Set cache expiration time
      expires: new Date('2028/01/01'),
      // Set the name of the downloaded content
      contentDisposition: 'example.png',
      // Set encoding type when downloading
      contentEncoding: 'deflate',
    });
    console.log('setObjectMeta Request ID:', requestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5p-l6K-i5a-56LGh5YWD5pWw5o2u5L-h5oGv77yI5Yik5pat5a-56LGh5piv5ZCm5a2Y5Zyo77yJ"></span>
### Query object metadata (determine whether the object exists)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must have <code>tos: GetObject</code>permission before getting object metadata, see <a href="https://docs.byteplus.com/docs/tos/docs-overview_6">Overview</a>.</div>


```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
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

const bucketName = 'node-sdk-test-bucket';
// Object name in the storage bucket.
const objectKey = 'example_dir/example.txt';
async function main() {
  try {
    const { headers, requestId } = await client.headObject({
      bucket: bucketName,
      key: objectKey,
    });
    console.log('headObject Request ID:', requestId);
    // View content language format
    console.log('headObject Response ContentLanguage:', headers['content-language']);
    // View the name when downloading
    console.log('headObject Response ContentDisposition:', headers['content-disposition']);
    // View encoding type
    console.log('headObject Response ContentEncoding:', headers['content-encoding']);
    // View caching strategy
    console.log('headObject Response CacheControl:', headers['cache-control']);
    // View object type
    console.log('headObject Response ContentType:', headers['content-type']);
    // View cache expiration time
    console.log('headObject Response Expires:', headers['expires']);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="86e186dd"></span>
## **Related documentation**

For API documentation on setting object metadata, see [SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta).
