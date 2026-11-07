---
title: "Managing Cross-Origin Resource Sharing (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-cross-origin-resource-sharing-node-js-sdk"
---

You can set Cross\-Origin Resource Sharing (CORS) rules through the SDK interface. When TOS receives a cross\-origin request or OPTIONS request, it will read the CORS rules corresponding to the bucket, perform corresponding permission checks and return corresponding headers to ensure the security of cross\-origin data transmission. This article describes how to configure CORS for buckets.

<span id=".6K6-572u6Leo5Z-f6LWE5rqQ5YWx5Lqr"></span>
## **Setting up CORS**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before setting up CORS rules for a bucket, you must have the <code>tos: PutBucketCORS</code>permission. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the CORS rules for a bucket.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError, HttpMethodType } from '@volcengine/tos-sdk';

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
async function main() {
  try {
    const corsRule1 = {
      // Set the allowed origins, * means allow all requests
      AllowedOrigins: ['*'],
      // Set the allowed methods, for example: GET, PUT, HEAD, POST, DELETE
      AllowedMethods: [HttpMethodType.HttpMethodGet, HttpMethodType.HttpMethodPut],
      // Set the custom HTTP request headers that the request can use
      AllowedHeaders: ['header1', 'header2'],
      // Set the custom headers from the server side that the browser can receive
      ExposeHeaders: ['tos-1', 'tos-2'],
      // Set the expiration time for the result of OPTIONS request
      MaxAgeSeconds: 100,
    };
    const corsRule2 = {
      AllowedOrigins: ['http://example.com', 'http://www.volcengine.com'],
      AllowedMethods: [HttpMethodType.HttpMethodGet, HttpMethodType.HttpMethodPut],
      AllowedHeaders: ['header1', 'header2'],
      ExposeHeaders: ['tos-1', 'tos-2'],
      MaxAgeSeconds: 100,
    };
    const { requestId: putCORSRequestId } = await client.putBucketCORS({
      bucket: bucketName,
      CORSRules: [corsRule1, corsRule2],
    });
    console.log('putBucketCORS Request ID: ', putCORSRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6I635Y-W6Leo5Z-f6LWE5rqQ5YWx5Lqr6YWN572u"></span>
## **Get CORS configuration**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must have the <code>tos: GetBucketCORS</code>permission before retrieving CORS rules for a bucket. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the CORS rules for a bucket.

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
async function main() {
  try {
    const { data, requestId: getCORSRequestId } = await client.getBucketCORS({
      bucket: bucketName,
    });
    console.log('getBucketCORS Request ID: ', getCORSRequestId);
    console.log('CORS Length:  ', data.CORSRules.length);
    // View detailed information on cross-origin access rules.
    for (const rule of data.CORSRules) {
      console.log('cors Rule AllowedOrigins:', rule.AllowedOrigins);
      console.log('cors Rule AllowedHeaders:', rule.AllowedHeaders);
      console.log('cors Rule ExposeHeaders:', rule.ExposeHeaders);
      console.log('cors Rule AllowedMethods:', rule.AllowedMethods);
      console.log('cors Rule MaxAgeSeconds:', rule.MaxAgeSeconds);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Yig6Zmk6Leo5Z-f6LWE5rqQ5YWx5Lqr6YWN572u"></span>
## **Delete CORS configuration**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must have the <code>tos: PutBucketCORS</code>permission before deleting CORS rules for a bucket. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to delete the CORS rule for a bucket.

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
async function main() {
  try {
    const { requestId: deleteCORSRequestId } = await client.deleteBucketCORS({
      bucket: bucketName,
    });
    console.log('deleteBucketCORS Request ID: ', deleteCORSRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information on CORS, see [CORS settings](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).
