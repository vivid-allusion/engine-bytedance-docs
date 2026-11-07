---
title: "List Objects V2 (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-v2-node-js-sdk"
---

This article describes how to list all objects in a specified bucket, prefix files, files in a specified directory, and subdirectories using listObjectsType2.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* The ListObjects interface has been revised to ListObjectsType2, and developers are strongly recommended to use ListObjectsType2. To ensure backward compatibility, TOS continues to support the ListObjects interface.

* To use the enumeration object V2, you must have `tos: ListBucket`permission, see [Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

ListObjectsType2 supports the following parameters:


|**parameter** |**describe** |
|---|---|
|Prefix |The prefix of this query result. |
|Delimiter |Characters to group object names. |
|StartAfter |The starting point for this list of objects. |
|ContinuationToken |Specifies that the enumeration operation needs to start with this token. Available from the NextContinuationToken in the last enumeration. |
|MaxKeys |Returns the maximum number of enumerated objects, the default is 1000.<br><br>Value: greater than 0 and less than or equal to 1000. |
|EncodingType |Encodes the returned content and specifies the type of encoding. The value selection description is as follows:<br><br><br>* `Undefined`: Default value, no encoding.<br><br>* `'Url '`: Encode the URL. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".566A5Y2V5YiX5Li-"></span>
### **Simple list**

The following code enumerates the specified bucket to get up to 10 objects.

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
    // Get up to 10 objects from the bucket.
    const { data } = await client.listObjectsType2({
      bucket: bucketName,
      maxKeys: 1000,
    });
    for (const obj of data.Contents) {
      // Object Key
      console.log('Object Key:', obj.Key);
      // Object LastModified
      console.log('Object LastModified:', obj.LastModified);
      // Object Etag
      console.log('Object ETag:', obj.ETag);
      // Object Size
      console.log('Object Size:', obj.Size);
      // Object Owner
      console.log('Object Owner:', obj.Owner);
      // Object StorageClass
       console.log('Object StorageClass:', obj.StorageClass);
      // Object CRC64
      console.log('Object HashCrc64ecma:', obj.HashCrc64ecma);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5YiG6aG15YiX5Li-"></span>
### **Paging list**

The following code is used to page out the objects in the specified bucket.

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
    // Get the first 1000 objects from the bucket.
    const { data } = await client.listObjectsType2({
      bucket: bucketName,
      maxKeys: 1000,
    });
    printObjectContents(data.Contents);

    // List the next 1000 objects after pagination.
    const { data: data2 } = await client.listObjectsType2({
      bucket: bucketName,
      maxKeys: 1000,
      continuationToken: data.NextContinuationToken,
    });
    printObjectContents(data2.Contents);
  } catch (error) {
    handleError(error);
  }
}

function printObjectContents(contents) {
  console.log('Contents Length:', contents.length);

  for (const obj of contents) {
    // Object Key
    console.log('Object Key:', obj.Key);
    // Object LastModified
    console.log('Object LastModified:', obj.LastModified);
    // Object ETag
    console.log('Object ETag:', obj.ETag);
    // Object Size
    console.log('Object Size:', obj.Size);
    // Object Owner
    console.log('Object Owner:', obj.Owner);
    // Object StorageClass
    console.log('Object StorageClass:', obj.StorageClass);
    // Object CRC64
    console.log('Object HashCrc64ecma:', obj.HashCrc64ecma);
  }
}

main();
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### **List all objects with the specified prefix**

The following code enumerates all objects with the specified prefix for the specified bucket.

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
    const prefix = '*** Provide your object key prefix ***';
    for (let truncated = true, continuationToken = ''; truncated; ) {
      const { data } = await client.listObjectsType2({
        bucket: bucketName,
        maxKeys: 1000,
        continuationToken: continuationToken,
        prefix,
      });
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
    // Object Key
    console.log('Object Key:', obj.Key);
    // Object LastModified
    console.log('Object LastModified:', obj.LastModified);
    // Object ETag
    console.log('Object ETag:', obj.ETag);
    // Object Size
    console.log('Object Size:', obj.Size);
    // Object Owner
    console.log('Object Owner:', obj.Owner);
    // Object StorageClass
    console.log('Object StorageClass:', obj.StorageClass);
    // Object CRC64
    console.log('Object HashCrc64ecma:', obj.HashCrc64ecma);
  }
}

main();
```


<span id=".5YiG6aG15YiX5Li-5qG25YaF5omA5pyJ5a-56LGh"></span>
### **Page list of all objects in the bucket**

The following code enumerates all the objects in the specified bucket.

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
    for (let truncated = true, continuationToken = ''; truncated; ) {
      const { data } = await client.listObjectsType2({
        bucket: bucketName,
        maxKeys: 1000,
        continuationToken: continuationToken,
      });
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
    // Object Key
    console.log('Object Key:', obj.Key);
    // Object LastModified
    console.log('Object LastModified:', obj.LastModified);
    // Object ETag
    console.log('Object ETag:', obj.ETag);
    // Object Size
    console.log('Object Size:', obj.Size);
    // Object Owner
    console.log('Object Owner:', obj.Owner);
    // Object StorageClass
    console.log('Object StorageClass:', obj.StorageClass);
    // Object CRC64
    console.log('Object HashCrc64ecma:', obj.HashCrc64ecma);
  }
}

main();
```


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
### **List the files and subdirectories in the specified directory**

TOS only has the concept of objects, and can simulate the functionality of directories by creating an object of size 0 and ending with a slash`/`.

By `delimiter`and `prefix`two parameters can simulate the function of the directory:


* First set `delimiter`to`/`and set `prefix`to empty to return the object and subdirectory information in the root directory.

* Set `delimiter`to`/`and set `prefix`as subfiledir to return the objects and subdirectories of the subdirectory.


The following code enumerates the objects and subdirectories in the root directory.

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
    // List the files and subdirectories in the directory.
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
    // Object Key
    console.log('Object Key:', obj.Key);
    // Object LastModified
    console.log('Object LastModified:', obj.LastModified);
    // Object Etag
    console.log('Object ETag:', obj.ETag);
    // Object Size
    console.log('Object Size:', obj.Size);
    // Object Owner
    console.log('Object Owner:', obj.Owner);
    // Object StorageClass
    console.log('Object StorageClass:', obj.StorageClass);
    // Object CRC64
    console.log('Object HashCrc64ecma:', obj.HashCrc64ecma);
  }
}

main();
```
