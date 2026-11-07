---
title: "Listing Objects with Multiple Versions (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-multi-version-objects-node-js-sdk"
---

This interface is used to enumerate multiversion objects in a bucket. Each request returns a portion of the bucket's multiversion objects (up to 1000 in a single request), and a subset of the objects in the bucket can be returned using request parameters as selection criteria.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Before enumerating multiversion objects, you need to have the `tos: ListBucket`permission, see [Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description


|parameter |describe |
|---|---|
|prefix |The prefix of this query result. |
|delimiter |Characters to group object names. |
|maxKeys |Returns the maximum number of enumerated objects, the default is 1000.<br><br>Value: (0, 1000] |
|encodingType |Encodes the returned content and specifies the type of encoding. The value selection description is as follows:<br><br><br>* `Undefined`: Default value, no encoding.<br><br>* `'Url '`: Encode the URL. |
|keyMarker |List the starting position of a multiversion object. Sets to return a list of objects sorted alphabetically from the value. Usually the `NextKeyMarker`value returned for the last request. |
|versionIdMarker |Used in conjunction with `keyMarker`, sets a dictionary\-sorted list of object pairs from this value. Gets from the `NextVersionIDMarker`from the last enumeration. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".566A5Y2V5YiX5Li-"></span>
### Simple list

The following code enumerates up to 10 multiversion objects in a specified bucket.

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
async function main() {
  try {
    // Get up to 10 multi-version objects from the bucket.
    const { data } = await client.listObjectVersions({
      bucket: bucketName,
      maxKeys: 1000,
    });
    printObjectVersions(data);
  } catch (error) {
    handleError(error);
  }
}

function printObjectVersions(data) {
  console.log('Versions.length:', data.Versions.length);
  for (const obj of data.Versions) {
    console.log('Obj Key:', obj.Key);
    console.log('Obj Version ID:', obj.VersionID);
    console.log('Obj Last Modified:', obj.LastModified);
    console.log('Obj Is Latest Version:', obj.IsLatest);
  }
  console.log('DeleteMarkers.length:', data.DeleteMarkers.length);
  for (const deleteMarker of data.DeleteMarkers) {
    console.log('Delete Maker Key:', deleteMarker.Key);
    console.log('Delete Maker Version ID:', deleteMarker.VersionID);
    console.log('Delete Maker Last Modified:', deleteMarker.LastModified);
    console.log('Delete Maker Is Latest Version:', deleteMarker.IsLatest);
  }
}

main();
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### List all objects with the specified prefix

The following code enumerates all multiversion objects and deletion tags under the specified prefix for the specified bucket.

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
async function main() {
  try {
    // List all multi-versioned objects with the specified prefix.
    const prefix = '*** Provide your object key prefix ***';
    for (let truncated = true, keyMarker = '', versionIdMarker = ''; truncated; ) {
      const { data } = await client.listObjectVersions({
        bucket: bucketName,
        maxKeys: 1000,
        prefix,
        keyMarker,
        versionIdMarker,
      });
      printObjectVersions(data);

      truncated = data.IsTruncated;
      keyMarker = data.NextKeyMarker;
      versionIdMarker = data.NextVersionIdMarker;
    }
  } catch (error) {
    handleError(error);
  }
}

function printObjectVersions(data) {
  console.log('Versions.length:', data.Versions.length);
  for (const obj of data.Versions) {
    console.log('Obj Key:', obj.Key);
    console.log('Obj Version ID:', obj.VersionID);
    console.log('Obj Last Modified:', obj.LastModified);
    console.log('Obj Is Latest Version:', obj.IsLatest);
  }
  console.log('DeleteMarkers.length:', data.DeleteMarkers.length);
  for (const deleteMarker of data.DeleteMarkers) {
    console.log('Delete Maker Key:', deleteMarker.Key);
    console.log('Delete Maker Version ID:', deleteMarker.VersionID);
    console.log('Delete Maker Last Modified:', deleteMarker.LastModified);
    console.log('Delete Maker Is Latest Version:', deleteMarker.IsLatest);
  }
}

main();
```


<span id=".5YiX5Li-5omA5pyJ5a-56LGh"></span>
### List all objects

The following code enumerates all multiversion objects and deletion tags in the specification bucket.

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
async function main() {
  try {
    // List all multi-version objects.
    for (let truncated = true, keyMarker = '', versionIdMarker = ''; truncated; ) {
      const { data } = await client.listObjectVersions({
        bucket: bucketName,
        maxKeys: 1000,
        keyMarker,
        versionIdMarker,
      });
      printObjectVersions(data);

      truncated = data.IsTruncated;
      keyMarker = data.NextKeyMarker;
      versionIdMarker = data.NextVersionIdMarker;
    }
  } catch (error) {
    handleError(error);
  }
}

function printObjectVersions(data) {
  console.log('Versions.length:', data.Versions.length);
  for (const obj of data.Versions) {
    console.log('Obj Key:', obj.Key);
    console.log('Obj Version ID:', obj.VersionID);
    console.log('Obj Last Modified:', obj.LastModified);
    console.log('Obj Is Latest Version:', obj.IsLatest);
  }
  console.log('DeleteMarkers.length:', data.DeleteMarkers.length);
  for (const deleteMarker of data.DeleteMarkers) {
    console.log('Delete Maker Key:', deleteMarker.Key);
    console.log('Delete Maker Version ID:', deleteMarker.VersionID);
    console.log('Delete Maker Last Modified:', deleteMarker.LastModified);
    console.log('Delete Maker Is Latest Version:', deleteMarker.IsLatest);
  }
}

main();
```


<span id="632f6569"></span>
### **Recursive list objects and subdirectories in a directory**

TOS only has the concept of objects, and can simulate the functionality of directories by creating an object of size 0 and ending with a slash`/`.

By `delimiter`and `prefix`two parameters can simulate the function of the directory:


* First set `delimiter`to`/`and set `prefix`to empty to return the object and subdirectory information in the root directory.

* Set `delimiter`to`/`and set `prefix`as subfiledir to return the objects and subdirectories of the subdirectory.


The following code is used to recursively list the objects and subdirectories in the directory. For all versions of the object information, the directory information only returns the latest version.

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
    // List all multi-version objects.
    for (let truncated = true, keyMarker = '', versionIdMarker = ''; truncated; ) {
      const { data } = await client.listObjectVersions({
        bucket: bucketName,
        maxKeys: 1000,
        keyMarker,
        versionIdMarker,
        delimiter: '/',
      });

      // Print multiple version objects under the root directory.
      console.log('Sub Dir Length:', data.CommonPrefixes.length);
      for (const prefix of data.CommonPrefixes) {
        console.log('Sub Dir:', prefix.Prefix);
      }
      // Print multiple version objects under the root directory.
      printObjectVersions(data);

      truncated = data.IsTruncated;
      keyMarker = data.NextKeyMarker;
      versionIdMarker = data.NextVersionIdMarker;
    }
  } catch (error) {
    handleError(error);
  }
}

function printObjectVersions(data) {
  console.log('Versions.length:', data.Versions.length);
  for (const obj of data.Versions) {
    console.log('Obj Key:', obj.Key);
    console.log('Obj Version ID:', obj.VersionID);
    console.log('Obj Last Modified:', obj.LastModified);
    console.log('Obj Is Latest Version:', obj.IsLatest);
  }
  console.log('DeleteMarkers.length:', data.DeleteMarkers.length);
  for (const deleteMarker of data.DeleteMarkers) {
    console.log('Delete Maker Key:', deleteMarker.Key);
    console.log('Delete Maker Version ID:', deleteMarker.VersionID);
    console.log('Delete Maker Last Modified:', deleteMarker.LastModified);
    console.log('Delete Maker Is Latest Version:', deleteMarker.IsLatest);
  }
}

main();
```


<span id="f725757a"></span>
## **Related documentation**

For API documentation that enumerates multiversion objects, see [ListObjectVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions).
