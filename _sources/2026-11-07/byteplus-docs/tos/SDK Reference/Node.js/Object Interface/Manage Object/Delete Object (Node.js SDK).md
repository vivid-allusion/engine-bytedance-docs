---
title: "Delete Object (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-objects-node-js-sdk"
---

When an object is no longer in use, you can delete it to reduce costs. The current TOS Node. JS SDK supports deleting a single object in a bucket and deleting a specified number of objects. For opening multiple versions of a bucket, you can specify to delete any version of the object's data.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Before deleting an object, you must have `tos: DeleteObject`permission. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).

* For multiple versions of buckets, you must have the `tos: DeleteObjectVersion`permission before deleting the specified version object. For details, see [Overview](https://docs.byteplus.com/docs/tos/docs--overview).


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5Yig6Zmk5oyH5a6a5a-56LGh"></span>
### Delete a specified object

The following code shows deleting the specified object from the bucket.

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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    // The specified objectKey
    const objectKey = '*** Provide your object key ***';

    // Delete object
    const { requestId } = await client.deleteObject({
      bucket: bucketName,
      key: objectKey,
    });
    console.log('deleteObject Request ID:', requestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="37bcf92d"></span>
### **Delete a specified object version**

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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    // Specified objectKey
    const objectKey = '*** Provide your object key ***';
    // Object version corresponding to objectKey
    const versionId = `*** Provide objectKey's version id ***`;

    // Delete object
    const { requestId } = await client.deleteObject({
      bucket: bucketName,
      key: objectKey,
      versionId,
    });
    console.log('deleteObject Request ID:', requestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="2406f85a"></span>
### **Batch delete objects**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">In the bucket with version control turned on, when the DeleteMultiObjects interface is called to delete objects in bulk, a deletion flag is inserted if <code>versionId</code>is not specified in the Delete request. If <code>versionId is specified</code>, the specified version of the object is permanently deleted.</div>


* <div data-tips="true" data-tips-type="warning">The response methods supported for bulk deletion of objects can be set by <code>quiet</code>:</div>


   * <div data-tips="true" data-tips-type="warning"><code>When quiet</code>is <code>false</code>, it means that when the response is returned, the deletion result will be included in the response regardless of whether the object is successfully deleted or not.</div>


   * <div data-tips="true" data-tips-type="warning"><code>When quiet</code>is <code>true</code>, it means that when the response is returned, only the result of deleting the object that failed is returned, and the deletion is not considered successful.</div>



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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    // Specified objectKey
    const objectKey1 = '*** Provide your object key ***';
    const objectKey2 = '*** Provide your object key ***';

    // Batch delete objects
    const { data, requestId } = await client.deleteMultiObjects({
      bucket: bucketName,
      objects: [{ key: objectKey1 }, { key: objectKey2 }],
    });
    console.log('deleteMultiObjects Request ID:', requestId);
    console.log('deleteMultiObjects Deleted.length:', data.Deleted.length);
    for (const item of data.Deleted) {
      console.log('deleted item Key:', item.Key);
      console.log('deleted item VersionId:', item.VersionId);
      console.log('deleted item DeleteMarker:', item.DeleteMarker);
      console.log('deleted item DeleteMarkerVersionId:', item.DeleteMarkerVersionId);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="e8a9fa62"></span>
### **Batch delete object versions**

The following code is used to delete multiple object data for the specified object name and version number in the specified bucket.

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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    // Specified objectKey
    const objectKey1 = '*** Provide your object key ***';
    const objectKey2 = '*** Provide your object key ***';
    // The specified version number.
    const versionId1 = `*** Provide objectKey1's version id ***`;
    const versionId2 = `*** Provide objectKey2's version id ***`;

    // Batch delete objects
    const { data, requestId } = await client.deleteMultiObjects({
      bucket: bucketName,
      objects: [
        { key: objectKey1, versionId: versionId1 },
        { key: objectKey2, versionId: versionId2 },
      ],
    });
    console.log('deleteMultiObjects Request ID:', requestId);
    console.log('deleteMultiObjects Deleted.length:', data.Deleted.length);
    for (const item of data.Deleted) {
      console.log('deleted item Key:', item.Key);
      console.log('deleted item VersionId:', item.VersionId);
      console.log('deleted item DeleteMarker:', item.DeleteMarker);
      console.log('deleted item DeleteMarkerVersionId:', item.DeleteMarkerVersionId);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="668156cd"></span>
### **Delete all objects in the bucket**

The following code shows deleting all objects in the specified bucket.

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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';

    for (let isTruncated = true, keyMarker = '', versionIdMarker = ''; isTruncated; ) {
      const { data } = await client.listObjectVersions({
        maxKeys: 1000,
        bucket: bucketName,
        keyMarker,
        versionIdMarker,
      });

      // Delete multiple versions of an object.
      for (const object of data.Versions) {
        const { requestId } = await client.deleteObject({
          bucket: bucketName,
          key: object.Key,
          versionId: object.VersionId,
        });
        console.log('deleteObject %s Request ID:', object.Key, requestId);
      }

      // Delete tag information.
      for (const markers of data.DeleteMarkers) {
        const { requestId } = await client.deleteObject({
          bucket: bucketName,
          key: markers.Key,
          versionId: markers.VersionId,
        });
        console.log('deleteObject DeleteMarker %s Request ID:', markers.Key, requestId);
      }
      isTruncated = data.IsTruncated;
      keyMarker = data.NextKeyMarker;
      versionIdMarker = data.NextVersionIdMarker;
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="4231c791"></span>
## **Related documentation**

For API documentation on deleting objects, see [DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject).
