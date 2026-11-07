---
title: "Directory Scenario (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Directory-scenes-node-js-sdk"
---

TOS employs only the concept of objects and stores data using a flat structure. To facilitate object grouping and simplify permission management, you can organize objects using a directory hierarchy.

<span id=".5Yib5bu655uu5b2V"></span>
## **Creating a Table of Contents**

```JavaScript
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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    const key = 'exampledir/';
    const { requestId: putObjectRequestId } = await client.putObject({
      bucket: bucketName,
      key,
    });
    console.log('putObject Request ID: ', putObjectRequestId);

    const key2 = 'exampledir/test/';
    const { requestId: putObjectRequestId2 } = await client.putObject({
      bucket: bucketName,
      key: key2,
    });
    console.log('putObject Request ID: ', putObjectRequestId2);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5qih5ouf55uu5b2V5p-l6K-i"></span>
## **Simulated Directory Query**

TOS only supports the concept of objects; it is possible to create an object with a size of 0 and a name that starts with a slash.`/`Objects at the end of the list simulate the function of a directory.

The functionality of a directory can be simulated using the `delimiter` and `prefix` parameters:


* First, set the `delimiter` to`/`At the same time, set `prefix` to empty to retrieve information about objects and subdirectories in the root directory.

* When setting `delimiter` to`/`By simultaneously setting `prefix` as a subdirectory (subfiledir), objects and subdirectories within the subdirectory can be returned.


The following code is used to enumerate objects and subdirectories in the root directory.

```JavaScript
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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    for (let truncated = true, continuationToken = ''; truncated; ) {
      const { data } = await client.listObjectsType2({
        bucket: bucketName,
        maxKeys: 1000,
        continuationToken: continuationToken,
        delimiter: '/',
      });

      console.log('Sub Dir Length:', data.CommonPrefixes.length);
      for (const prefix of data.CommonPrefixes) {
        console.log('Sub Dir:', prefix.Prefix);
      }
      printObjectContents(data.Contents);

      truncated = data.IsTruncated;
      continuationToken = data.NextContinuationToken;
    }
  } catch (error) {
    handleError(error);
  }
}

function printObjectContents(contents) {
  console.log('Contents Length:', contents.length);

  for (const obj of contents) {
    console.log('Object Key:', obj.Key);
    console.log('Object LastModified:', obj.LastModified);
    console.log('Object ETag:', obj.ETag);
    console.log('Object Size:', obj.Size);
    console.log('Object Owner:', obj.Owner);
    console.log('Object StorageClass:', obj.StorageClass);
    console.log('Object HashCrc64ecma:', obj.HashCrc64ecma);
  }
}

main();
```


<span id=".5Yig6Zmk55uu5b2V5LiL55qE5paH5Lu2"></span>
## **Delete files in the directory.** 

The following code is used to delete all files under the `exampledir/` directory in the storage bucket.

```JavaScript
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

const bucketName = 'node-sdk-test-bucket';
async function main() {
  try {
    const dir = 'exampledir/';
    for (let truncated = true, continuationToken = ''; truncated; ) {
      const { data } = await client.listObjectsType2({
        bucket: bucketName,
        maxKeys: 1000,
        continuationToken: continuationToken,
        prefix: dir,
      });

      for (const obj of data.Contents) {
        const { requestId } = await client.deleteObject({
          bucket: bucketName,
          key: obj.Key,
        });
        console.log('deleteObject %s Request ID:', obj.Key, requestId);
      }
      truncated = data.IsTruncated;
      continuationToken = data.NextContinuationToken;
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```
