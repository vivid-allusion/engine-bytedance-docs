---
title: "Managing Static Websites (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-static-websites-node-js-sdk"
---

TOS supports hosting static websites. You can store all the content of a static website in a TOS bucket. After configuring static website rules, you can access the website through the bucket domain name.

<span id=".6K6-572u572R56uZ6YWN572u6KeE5YiZ"></span>
## **Set up website configuration rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only one static website hosting rule can be created in a bucket.</div>


* <div data-tips="true" data-tips-type="warning">After setting up a static website, a custom domain name must be bound to take effect.</div>


* <div data-tips="true" data-tips-type="warning">For security compliance reasons, starting from October 18, 2022, if you use the default domain name of the bucket to access the webpage type file (mimetype is text/html, the extension includes HTM, HTML, JSP, PLG, HTX, STM), the Response Header will automatically add <code>Content-Disposition: attachment</code>, that is, when accessing the webpage type file from the browser, the website will not be previewed directly, but the content of the website will be downloaded locally.</div>



<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to redirect all requests to another site.

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
    // Scene 1: Redirect all requests to another website.
    const { requestId: putWebsiteRequestId } = await client.putBucketWebsite({
      bucket: bucketName,
      redirectAllRequestsTo: {
        HostName: 'www.example.com',
        Protocol: 'http',
      },
    });
    console.log('putBucketReplication Request ID: ', putWebsiteRequestId);

    // Scene 2: Redirecting requests according to the rules.
    const { requestId: putWebsiteRequestId2 } = await client.putBucketWebsite({
      bucket: bucketName,
      indexDocument: {
        Suffix: 'index.html',
      },
      errorDocument: {
        Key: 'error.html',
      },
      // Prefix matching, obtain redirection results.
      routingRules: [
        {
          // Configuration of conditions for redirect rules
          Condition: {
            // Matching condition for object key prefix of the specified redirect rule
            KeyPrefixEquals: 'prefix',
            // Matching condition for error code of the specified redirect rule
            HttpErrorCodeReturnedEquals: 403,
          },
          // Specific redirection target configuration for redirection rules.
          Redirect: {
            // Target protocol for specifying redirection rules.
            Protocol: 'https',
            HostName: 'www.redirect.com',
          },
        },
      ],
    });
    console.log('putBucketReplication Request ID: ', putWebsiteRequestId2);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6I635Y-W572R56uZ6YWN572u6KeE5YiZ"></span>
## **Get website configuration rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To get the bucket's site configuration rules, by default you must be the bucket owner.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to obtain the website configuration rules for the bucket.

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
    const { data, requestId: getWebsiteRequestId } = await client.getBucketWebsite({
      bucket: bucketName,
    });
    console.log('getBucketWebsite Request ID: ', getWebsiteRequestId);

    if (data.RedirectAllRequestsTo != null) {
      console.log('getBucketWebsite RedirectAllRequestsTo HostName:', data.RedirectAllRequestsTo.HostName);
      console.log('getBucketWebsite RedirectAllRequestsTo Protocol:', data.RedirectAllRequestsTo.Protocol);
    }

    if (data.IndexDocument != null) {
      console.log('getBucketWebsite IndexDocument ForbiddenSubDir:', data.IndexDocument.ForbiddenSubDir);
      console.log('getBucketWebsite IndexDocument Suffix:', data.IndexDocument.Suffix);
    }

    if (data.ErrorDocument != null) {
      console.log('getBucketWebsite ErrorDocument Key:', data.ErrorDocument.Key);
    }

    for (const rule of data.RoutingRules || []) {
      console.log('getBucketWebsite RoutingRules Rule Condition HttpErrorCodeReturnedEquals:', rule.Condition.HttpErrorCodeReturnedEquals);
      console.log('getBucketWebsite RoutingRules Rule Condition KeyPrefixEquals:', rule.Condition.KeyPrefixEquals);
      console.log('getBucketWebsite RoutingRules Rule Redirect HostName:', rule.Redirect.HostName);
      console.log('getBucketWebsite RoutingRules Rule Redirect Protocol:', rule.Redirect.Protocol);
      console.log('getBucketWebsite RoutingRules Rule Redirect ReplaceKeyWith:', rule.Redirect.ReplaceKeyWith);
      console.log('getBucketWebsite RoutingRules Rule Redirect ReplaceKeyPrefixWith:', rule.Redirect.ReplaceKeyPrefixWith);
      console.log('getBucketWebsite RoutingRules Rule Redirect HttpRedirectCode:', rule.Redirect.HttpRedirectCode);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Yig6Zmk572R56uZ6YWN572u6KeE5YiZ"></span>
## **Delete website configuration rules**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To remove a bucket's site configuration rule, you must be the bucket owner by default.</div>


<span id=".56S65L6L5Luj56CB"></span>
### **Sample code**

The following code is used to delete the bucket's site configuration rule.

```go
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
    const { requestId: deleteWebsiteRquestId } = await client.deleteBucketWebsite({
      bucket: bucketName,
    });
    console.log('deleteBucketWebsite Request ID: ', deleteWebsiteRquestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```
