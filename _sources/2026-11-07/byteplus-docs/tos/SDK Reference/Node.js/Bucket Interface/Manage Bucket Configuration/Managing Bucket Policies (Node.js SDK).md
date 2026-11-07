---
title: "Managing Bucket Policies (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-strategy-node-js-sdk"
---

Bucket is the globally unique namespace of TOS, which is equivalent to a data container and is used to store object data. In TOS, permission control is realized by IAM Policy, bucket Policy, bucket and object ACL. Bucket Policy and ACL are both rights control policies based on TOS resources. Compared with bucket ACL, bucket Policy has more flexible rights configuration. This article describes how to set, obtain, and delete the authorization policy for a bucket.

<span id=".6K6-572u5a2Y5YKo5qG2562W55Wl"></span>
## **Set bucket policy**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Before setting a bucket policy, you must have <code>tos: PutBucketPolicy</code>permission, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


* <div data-tips="true" data-tips-type="warning">Users with the <code>tos: PutBucketPolicy</code>permission can change the bucket policy arbitrarily, and can obtain other permissions through this permission. It is recommended that you configure it carefully.</div>



<span id="579c0b1d"></span>
### Sample code

The following code sets the bucket policy.

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
    const { requestId: putPolicyRequestId } = await client.putBucketPolicy({
      bucket: bucketName,
      policy: {
        Statement: [
          {
            Sid: 'internal public',
            Effect: 'Allow',
            Action: ['*'],
            Principal: '*',
            Resource: [`trn:tos:::${bucketName}/*`, `trn:tos:::${bucketName}`],
          },
        ],
      },
    });
    console.log('putBucketPolicy Request ID: ', putPolicyRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6I635Y-W5a2Y5YKo5qG2562W55Wl"></span>
## **Get bucket policy**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must have the <code>tos: GetBucketPolicy permission</code> before you can get the bucket policy, see <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions Configuration Guide</a>.</div>


<span id="8ccbddc8"></span>
### Sample code

The following code is used to obtain the bucket policy.

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
    const { data, requestId: getPolicyRequestId } = await client.getBucketPolicy(bucketName);
    console.log('getBucketPolicy Request ID: ', getPolicyRequestId);
    console.log('Policy: %o', data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Yig6Zmk5a2Y5YKo5qG2562W55Wl"></span>
## **Delete bucket policy**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting a bucket policy, you must have <code>tos: DeleteBucketPolicy</code>permission, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


<span id="8abf8915"></span>
### Sample code

The following code is used to delete the bucket policy.

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
    const { requestId: deletePolicyRequestId } = await client.deleteBucketPolicy(bucketName);
    console.log('deleteBucketPolicy Request ID: ', deletePolicyRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For more information on bucket policies, see [Bucket Authorization Policy Management](https://docs.byteplus.com/docs/tos/docs-bucket-authorization-policy-management).
