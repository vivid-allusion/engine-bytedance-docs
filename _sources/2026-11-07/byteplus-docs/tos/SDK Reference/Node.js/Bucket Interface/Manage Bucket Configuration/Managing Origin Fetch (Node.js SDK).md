---
title: "Managing Origin Fetch (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-image-return-to-source-node-js-sdk"
---

Mirroring back to the source is mainly used for scenarios where data is seamlessly migrated to TOS. For example, if the web service is already running on your own source site, and you migrate the static web page to the TOS storage, you can configure the mirror back to the source rule to obtain some data that has not been migrated to the TOS.

<span id=".6K6-572u6ZWc5YOP5Zue5rqQ"></span>
## **Set mirror return to source**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A bucket only supports the creation of a back\-to\-source rule.</div>


* <div data-tips="true" data-tips-type="warning">Mirroring back to the source can support up to 5GiB of objects. If you need to request objects larger than 5GiB, use <a href="https://docs.byteplus.com/docs/tos/Scope-download-node-js-sdk">Scope Download (Node.js SDK)</a> Function.</div>


* <div data-tips="true" data-tips-type="warning">Redirecting back to the source can support up to 300GiB.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code sets the mirroring back\-to\-source rule for the specified bucket.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError, RedirectType } from '@volcengine/tos-sdk';

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
    const mirrorRule = {
      // Rule ID
      ID: 'rule1',
      Condition: {
        // The error code that triggers the origin-pull rule currently only supports 404.
        HttpCode: 404,
      },
      Redirect: {
        // Redirect rule type
        RedirectType: RedirectType.Mirror,
        // Whether to fetch data from the configured origin server after redirection
        FetchSourceOnRedirect: true,
        // Whether to include request parameters when performing redirection
        PassQuery: true,
        // When the mirror source result is 3XX, whether to redirect to Location to fetch data
        FollowRedirect: true,
        MirrorHeader: {
          // Whether to pass all HTTP headers to the origin server
          PassAll: false,
          // Pass specified headers to the origin server
          Pass: ['header-1', 'header-2'],
          // Disable passing specified headers to the origin server
          Remove: ['header-3', 'header-4'],
        },
        // Publicly accessible source address.
        PublicSource: {
          SourceEndpoint: {
            Primary: ['https://www.example.com'],
          },
        },
      },
    };
    const { requestId: putMirrorBackRequestId } = await client.putBucketMirrorBack({
      bucket: bucketName,
      rules: [mirrorRule],
    });
    console.log('putBucketMirrorBack Request ID: ', putMirrorBackRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6I635Y-W6ZWc5YOP5Zue5rqQ"></span>
## **Get mirror back to source**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must be the owner of the bucket in order to obtain the bucket's mirroring back\-to\-source rule.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the mirror back\-to\-source rule for the specified bucket.

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
    const { data, requestId: getMirrorBackRequestId } = await client.getBucketMirrorBack({
      bucket: bucketName,
    });
    console.log('getBucketMirrorBack Request ID: ', getMirrorBackRequestId);
    console.log('getBucketMirrorBack Rules Length: ', data.Rules.length);
    for (const rule of data.Rules) {
      // View rule ID
      console.log('rule ID:', rule.ID);
      // View the error code that triggers the origin-pull rule, currently only supports 404
      console.log('rule Condition HttpCode:', rule.Condition.HttpCode);
      // View the redirect type of the origin-pull rule
      console.log('rule Redirect RedirectType:', rule.Redirect.RedirectType);
      // Whether to fetch data from the origin server after redirection
      console.log('rule Redirect FetchSourceOnRedirect:', rule.Redirect.FetchSourceOnRedirect);
      // Whether to carry request parameters when performing redirection
      console.log('rule Redirect PassQuery:', rule.Redirect.PassQuery);
      // When the mirror origin result is 3XX, whether to redirect to Location to obtain data
      console.log('rule Redirect FollowRedirect:', rule.Redirect.FollowRedirect);
       // Whether to pass all HTTP headers to the origin server
      console.log('rule Redirect MirrorHeader PassAll:', rule.Redirect.MirrorHeader.PassAll);
      // Pass specified headers to the origin server
      console.log('rule Redirect MirrorHeader Pass:', rule.Redirect.MirrorHeader.Pass);
       // Prohibit passing specified headers to the origin server
      console.log('rule Redirect MirrorHeader Remove:', rule.Redirect.MirrorHeader.Remove);
      // Publicly accessible origin server address
      console.log('rule Redirect PublicSource SourceEndpoint:', rule.Redirect.PublicSource.SourceEndpoint);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Yig6Zmk6ZWc5YOP5Zue5rqQ"></span>
## **Delete mirror return to source**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must be the owner of the bucket in order to remove the bucket's mirroring back\-to\-source rule.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code deletes the mirror return rule for the specified bucket:

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
    const { requestId: deleteMirrorBackRequestId } = await client.deleteBucketMirrorBack({
      bucket: bucketName,
    });
    console.log('deleteBucketMirrorBack Request ID: ', deleteMirrorBackRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

For more information on mirroring back to the source, see [Setting Back-to-Origin Rules](https://docs.byteplus.com/docs/tos/docs-setting-back-to-origin-rules).
