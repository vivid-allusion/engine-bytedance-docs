---
title: "Quick Start (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start-node-js-sdk"
---

This article describes how to use the TOS Node.js SDK to perform basic operations, such as creating buckets, uploading, downloading, and deleting objects.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Installing the SDK](https://docs.byteplus.com/docs/tos/Install-the-node-js-sdk)

2. [Initialize Client](https://docs.byteplus.com/docs/tos/Initializing-the-client-side-node-js-sdk)


<span id=".5Yib5bu65a2Y5YKo5qG2"></span>
## Creating buckets

A bucket in TOS serves as a globally unique namespace, functioning as a data container for storing object data. The following code demonstrates how to create a new bucket.

```javascript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'], 
  accessKeySecret: process.env['TOS_SECRET_KEY'], 
  region: "Provide your region", 
  endpoint: "Provide your endpoint", 
});
const bucketName = 'node-sdk-test-bucket';

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
    await client.createBucket({
      bucket: bucketName,
    });
    const { data } = await client.listBuckets();

    const theBucket = data.Buckets.find(it => it.Name === bucketName);
    console.log('the bucket info', theBucket);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5LiK5Lyg5a-56LGh"></span>
## Uploads an object.

After successfully creating a bucket, you can upload objects to it. The following section demonstrates how to upload an object to an existing bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more examples of uploading objects, see <a href="https://docs.byteplus.com/docs/tos/Upload-object-overview-node-js-sdk">Uploading Objects</a>.</div>


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
    const objectName = 'example_dir/example.txt';
    await client.putObject({
      bucket: bucketName,
      key: objectName,
      body: Buffer.from('hello world'),
    });

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


<span id=".5LiL6L295a-56LGh"></span>
## Download Object

The following code demonstrates how to download an existing object from a bucket.

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
    const objectName = 'putObject-test'; 
    const {
      data: { content },
    } = await client.getObjectV2({
      bucket: bucketName,
      key: objectName,
    });

    let allContent = Buffer.from([]);
    for await (const chunk of content) {
      allContent = Buffer.concat([allContent, chunk]);
    }

    console.log('object size:', allContent.length);
    console.log('data string:', allContent.toString());
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5YiX5Li-5a-56LGh"></span>
## Enumerated Objects

The following lists the objects that have already been uploaded to the bucket.

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
    const { data } = await client.listObjects({
      bucket: bucketName,
      maxKeys: 10,
    });
    console.log(`listObjects bucketName:${bucketName} data: `, data);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Yig6Zmk5a-56LGh"></span>
## When you delete an object

The following code demonstrates how to delete an existing object from a bucket.

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
    const objectName = 'putObject-test'; 

    const { data } = await client.deleteObject({
      bucket: bucketName,
      key: objectName,
    });
    console.log(`deleteObject bucketName:${bucketName} key:${objectName} result: `, data);
  } catch (error) {
    handleError(error);
  }
}

main();
```
