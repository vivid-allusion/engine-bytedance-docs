---
title: "Enumerating Multi-Version Objects (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-multi-version-objects-harmony-sdk"
---

This interface is used to list multi\-version objects in a bucket. Each request returns a subset of multi\-version objects from the bucket, with a maximum of 1,000 objects per request. Request parameters can be used as selection criteria to return a specific subset of objects within the bucket.

<span id="9726ca8d"></span>
## Precautions

Before listing multi\-version objects, you must have the `tos:ListBucket` permission. For specific operations, refer to [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id="63cca2bb"></span>
## Parameter Description


|Parameters |Description |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |Character used to group object names. |
|maxKeys |Returns the maximum number of objects to be listed. The default value is 1000, and the valid range is (0, 1000]. |
|encodingType |Encode the returned content and specify the encoding type. The value description is as follows:<br><br><br>* `undefined`: Default value, no encoding.<br><br>* `'url'`: Use URL encoding. |
|keyMarker |Enumerate the starting positions of multi\-version objects. Return a list of objects sorted alphabetically, starting after the specified value. This is typically the `NextKeyMarker` value returned by the previous request. |
|versionIdMarker |Used in conjunction with `keyMarker`, this sets the operation to return a list of version objects sorted lexicographically, starting after the specified value. Obtain `NextVersionIDMarker` from the previous listing results. |


<span id="54ab7335"></span>
## Sample Code

<span id="fbc48c09"></span>
### Brief Enumeration

The following code is used to list up to 1,000 multi\-version objects in the bucket named bucketName.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
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

function printObjectVersions(data: ListObjectVersionsOutput) {
  console.log('Versions.length:', data.Versions.length);
  for (const obj of data.Versions) {
    console.log('Obj Key:', obj.Key);
    console.log('Obj Version ID:', obj.VersionId);
    console.log('Obj Last Modified:', obj.LastModified);
    console.log('Obj Is Latest Version:', obj.IsLatest);
  }
  console.log('DeleteMarkers.length:', data.DeleteMarkers.length);
  for (const deleteMarker of data.DeleteMarkers) {
    console.log('Delete Maker Key:', deleteMarker.Key);
    console.log('Delete Maker Version ID:', deleteMarker.VersionId);
    console.log('Delete Maker Last Modified:', deleteMarker.LastModified);
    console.log('Delete Maker Is Latest Version:', deleteMarker.IsLatest);
  }
}

async function main() {
  try {
   
    const res = await client.listObjectVersions({
      Bucket: bucketName,
      MaxKeys: 1000,
    });
    printObjectVersions(res);
  } catch (error) {
    handleError(error);
  }
}

main()
```


<span id="84c11cad"></span>
### List all objects with the specified prefix

The following code is used to list all multi\-version objects with the prefix 'prefix' in the 'bucketName' bucket.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
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

function printObjectVersions(data: ListObjectVersionsOutput) {
  console.log('Versions.length:', data.Versions.length);
  for (const obj of data.Versions) {
    console.log('Obj Key:', obj.Key);
    console.log('Obj Version ID:', obj.VersionId);
    console.log('Obj Last Modified:', obj.LastModified);
    console.log('Obj Is Latest Version:', obj.IsLatest);
  }
  console.log('DeleteMarkers.length:', data.DeleteMarkers.length);
  for (const deleteMarker of data.DeleteMarkers) {
    console.log('Delete Maker Key:', deleteMarker.Key);
    console.log('Delete Maker Version ID:', deleteMarker.VersionId);
    console.log('Delete Maker Last Modified:', deleteMarker.LastModified);
    console.log('Delete Maker Is Latest Version:', deleteMarker.IsLatest);
  }
}

const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {
  try {
    
    const prefix = '*** Provide your object key prefix ***';
    let keyMarker = ''
    let versionIdMarker = '';
    while (true) {
      const res = await client.listObjectVersions({
        Bucket: bucketName,
        MaxKeys: 1000,
        Prefix: prefix,
        KeyMarker: keyMarker,
        VersionIDMarker: versionIdMarker,
      });
      printObjectVersions(res);
      if (!res.IsTruncated) {
        break;
      }

      keyMarker = res.NextKeyMarker ?? '';
      versionIdMarker = res.NextVersionIdMarker ?? '';
    }
  } catch (error) {
    handleError(error);
  }
}

main()
```


<span id="e021346f"></span>
### List all objects

The following code is used to enumerate all multi\-version objects within the bucket named bucketName.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
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

function printObjectVersions(data: ListObjectVersionsOutput) {
  console.log('Versions.length:', data.Versions.length);
  for (const obj of data.Versions) {
    console.log('Obj Key:', obj.Key);
    console.log('Obj Version ID:', obj.VersionId);
    console.log('Obj Last Modified:', obj.LastModified);
    console.log('Obj Is Latest Version:', obj.IsLatest);
  }
  console.log('DeleteMarkers.length:', data.DeleteMarkers.length);
  for (const deleteMarker of data.DeleteMarkers) {
    console.log('Delete Maker Key:', deleteMarker.Key);
    console.log('Delete Maker Version ID:', deleteMarker.VersionId);
    console.log('Delete Maker Last Modified:', deleteMarker.LastModified);
    console.log('Delete Maker Is Latest Version:', deleteMarker.IsLatest);
  }
}

const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {
  try {
    
    let keyMarker = ''
    let versionIdMarker = '';
    while (true) {
      const res = await client.listObjectVersions({
        Bucket: bucketName,
        MaxKeys: 1000,
        KeyMarker: keyMarker,
        VersionIDMarker: versionIdMarker,
      });
      printObjectVersions(res);
      if (!res.IsTruncated) {
        break;
      }

      keyMarker = res.NextKeyMarker ?? '';
      versionIdMarker = res.NextVersionIdMarker ?? '';
    }
  } catch (error) {
    handleError(error);
  }
}

main()
```


<span id="5b23e3e5"></span>
### **Recursively enumerate objects and subdirectories within a directory**

TOS defines only the concept of objects; it is possible to create an object with a size of zero and a slash in its name.`/`The object at the end simulates the functionality of a directory.

The functionality of a directory can be simulated using the `delimiter` and `prefix` parameters:


* First, set the `delimiter` to`/`At the same time, if `prefix` is set to empty, information about objects and subdirectories in the root directory can be returned.

* When setting `delimiter` to`/`When `prefix` is set to a subdirectory (subfiledir), objects and subdirectories within that subdirectory can be returned.


The following code recursively enumerates the objects and subdirectories in the root directory of the bucket named bucketName. During enumeration, all versions of objects are returned, while only the latest version of directories is returned.

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
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

function printObjectVersions(data: ListObjectVersionsOutput) {
  console.log('Versions.length:', data.Versions.length);
  for (const obj of data.Versions) {
    console.log('Obj Key:', obj.Key);
    console.log('Obj Version ID:', obj.VersionId);
    console.log('Obj Last Modified:', obj.LastModified);
    console.log('Obj Is Latest Version:', obj.IsLatest);
  }
  console.log('DeleteMarkers.length:', data.DeleteMarkers.length);
  for (const deleteMarker of data.DeleteMarkers) {
    console.log('Delete Maker Key:', deleteMarker.Key);
    console.log('Delete Maker Version ID:', deleteMarker.VersionId);
    console.log('Delete Maker Last Modified:', deleteMarker.LastModified);
    console.log('Delete Maker Is Latest Version:', deleteMarker.IsLatest);
  }
}

async function main() {
  try {
   
    let keyMarker = '';
    let versionIdMarker = '';
    while (true) {
      const res = await client.listObjectVersions({
        Bucket: bucketName,
        MaxKeys: 1000,
        KeyMarker: keyMarker,
        VersionIDMarker: versionIdMarker,
        Delimiter: '/',
      });

    
      console.log('Sub Dir Length:', res.CommonPrefixes.length);
      for (const prefix of res.CommonPrefixes) {
        console.log('Sub Dir:', prefix.Prefix);
      }
   
      printObjectVersions(res);

      if (!res.IsTruncated) {
        break;
      }
      keyMarker = res.NextKeyMarker ?? '';
      versionIdMarker = res.NextVersionIdMarker ?? '';
    }
  } catch (error) {
    handleError(error);
  }
}

main()
```


<span id="3a82d3b6"></span>
## **Relevant Documentation**

For API documentation on listing multi\-version objects, refer to [ListObjectsVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions).
