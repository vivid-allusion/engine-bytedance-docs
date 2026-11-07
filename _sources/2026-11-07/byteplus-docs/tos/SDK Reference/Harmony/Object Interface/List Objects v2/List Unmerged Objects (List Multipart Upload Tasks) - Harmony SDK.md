---
title: "List Unmerged Objects (List Multipart Upload Tasks) - Harmony SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-unmerged-objects"
---

This interface is used to list unmerged objects in a bucket, that is, to enumerate multipart upload tasks.

<span id="ebcc5de5"></span>
## Precautions

Before listing multipart upload tasks, you must have the `tos:ListBucketMultipartUploads` permission. For details on specific operations, refer to [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id="7f61b4a0"></span>
## Parameter Description


|Parameters |Description |
|---|---|
|delimiter |Character used to group object names. |
|encodingType |Encode the returned content and specify the encoding type. Explanation of value assignments is as follows:<br><br><br>* `undefined`: default value, no encoding.<br><br>* `'url'`: Use URL encoding. |
|maxUploads |Returns the maximum number of multipart upload tasks. The default value is 1000, with an allowable range of (0, 1000]. |
|prefix |Used to specify the prefix name for enumerating returned objects. |
|keyMarker |List the starting positions of multipart upload tasks. Return a list of objects sorted alphabetically, starting after the specified value. Usually the value of `nextMarker` returned by the previous request. |
|uploadIDMarker |When used in conjunction with `keyMarker`, this specifies that the list of multipart upload tasks will be returned sorted lexicographically, starting after this value. Obtain `nextVersionIdMarker` from the results of the previous listing. |


<span id="fc83f064"></span>
## Sample Code

<span id="9579cc0d"></span>
### Brief Enumeration

The following code is used to list up to 1,000 unmerged multipart upload tasks in the storage bucket named 'bucketName'.

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

async function main() {
  try {
  
    const res = await client.listMultipartUploads({
      Bucket: bucketName,
      MaxUploads: 1000
    });

    console.log('Uploads.length:', res.Uploads.length);
    for (const upload of res.Uploads) {
      console.log('Object Key:', upload.Key);
      console.log('UploadID:', upload.UploadId);
      console.log('Owner:', upload.Owner);
      console.log('StorageClass:', upload.StorageClass);
    }
  } catch (error) {
    handleError(error);
  }
}

main()
```


<span id="6958269f"></span>
### List all unmerged shard tasks with the specified prefix.

The following code is used to enumerate all unmerged multipart upload tasks with the prefix 'prefix' in the storage bucket 'bucketName'.

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

async function main() {
  try {

    const prefix = '*** Provide your object key prefix ***';
    let keyMarker: string= ''
    let uploadIdMarker: string = '';
    while (true)  {
      const res = await client.listMultipartUploads({
        Bucket: bucketName,
        MaxUploads: 1000,
        Prefix: prefix,
        KeyMarker: keyMarker,
        UploadIdMarker: uploadIdMarker,
      });

      console.log('Uploads.length:', res.Uploads.length);
      for (const upload of res.Uploads) {
        console.log('Object Key:', upload.Key);
        console.log('UploadID:', upload.UploadId);
        console.log('Owner:', upload.Owner);
        console.log('StorageClass:', upload.StorageClass);
      }

      if (!res.IsTruncated) {
        break;
      }

      keyMarker = res.NextKeyMarker ?? '';
      uploadIdMarker = res.NextUploadIdMarker ?? '';
    }
  } catch (error) {
    handleError(error);
  }
}

main()
```


<span id="f62b3fac"></span>
### List all multipart upload tasks

The following code is used to list all unmerged multipart upload tasks in the storage bucket named bucketName \*\*\*\*.

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

async function main() {
  try {
    let keyMarker: string= ''
    let uploadIdMarker: string = '';
    while (true)  {
      const res = await client.listMultipartUploads({
        Bucket: bucketName,
        MaxUploads: 1000,
        KeyMarker: keyMarker,
        UploadIdMarker: uploadIdMarker,
      });

      console.log('Uploads.length:', res.Uploads.length);
      for (const upload of res.Uploads) {
        console.log('Object Key:', upload.Key);
        console.log('UploadID:', upload.UploadId);
        console.log('Owner:', upload.Owner);
        console.log('StorageClass:', upload.StorageClass);
      }

      if (!res.IsTruncated) {
        break;
      }

      keyMarker = res.NextKeyMarker ?? '';
      uploadIdMarker = res.NextUploadIdMarker ?? '';
    }
  } catch (error) {
    handleError(error);
  }
}

main()
```
