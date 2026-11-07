---
title: "Managed Object Metadata (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-metadata-harmony-sdk"
---

Object metadata describes the properties of an object and includes both HTTP standard attributes (HTTP Header) and user\-defined metadata (User Meta).

<span id="2da67a8b"></span>
## Precautions


* Only the object owner has permission to set object metadata.

* When setting user\-defined metadata, the Key (which uses English letters) supports only lowercase letters and does not allow spaces or other special characters.


<span id="f696aac0"></span>
## Parameter Description

The TOS Harmony SDK enables the addition and modification of metadata for objects that have already been uploaded. TOS supports the use of the following seven request headers to modify object metadata. When downloading an object or performing a HEAD request, these values are set in the HTTP header fields and returned to the client. The request headers are as follows:


|**Content\-Type** |**Object Type** |
|---|---|
|Cache\-Control |Specify the web page's caching behavior when this object is downloaded. |
|Expires |Cache expiration time as defined in RFC2616. |
|Content\-Disposition |Name assigned to the object upon download. |
|Content\-Encoding |Content encoding type applied when the object is downloaded. |
|Content\-Language |Content language format when the object is downloaded. |
|x\-tos\-meta\-\* |Metadata information set when configuring the `meta` field using the SDK. When this object is queried, the metadata will be included in the Header of the response message. |


<span id="e7ee2938"></span>
## Sample Code

<span id="e8a58358"></span>
### Setting Metadata Information During Standard Upload

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
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Header:', error.headers);
    console.log('Response Err Code:', error.code);
    console.log('Response Err Msg:', error.message);
  } else {
    console.log('unexpected exception, message: ', error);
  }
}

async function main() {
  const meta: Record<string, string> = {};
  meta.key = 'value';
  try {
    const res = await client.putObject({
      Bucket: bucketName,
      Key: objectKey,
      Content: buffer.from('Hello TOS').buffer,
      
      Meta: meta,
      
      ContentType: 'text/html',
      
      ContentLanguage: 'zh-cn',
      
      CacheControl: 'no-store',
      
      Expires: new Date('2028/01/01'),
      
      ContentDisposition: 'example.png',
      
      ContentEncoding: 'deflate',
    });
    console.log('putObject Request ID:', res.RequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="47e75672"></span>
### **Configuring Metadata for Multipart Uploads**

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
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
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
    const bucketName = 'harmony-sdk-test-bucket';
    const objectName = 'example_dir/multipartExample';
    
    const filePath = './example_dir/multipartExample';
    
    const meta: Record<string, string> = {};
    meta.key = 'value';
    const res = await client.createMultipartUpload({
      Bucket: bucketName,
      Key: objectName,
      Meta: meta,
      
      ContentType: 'text/html',
      
      ContentLanguage: 'zh-cn',
      
      CacheControl: 'no-store',
  
      Expires: new Date('2028/01/01'),
      
      ContentDisposition: 'example.png',
     
      ContentEncoding: 'deflate',
    });
    console.log('CreateMultipartUploadV2 Upload ID:', res.UploadId);

    
    const stats = await fs.statSync(filePath);
   
    const totalSize = stats.size;
  
    const partSize = 5 * 1024 * 1024;
    let offset = 0;
    
    let partNumber = 1;
    const partsInfo: UploadedPart[] = [];
    while (offset < totalSize) {
      const uploadResult = await client.uploadPart({
        Bucket: bucketName,
        Key: objectName,
        PartNumber: partNumber,
        UploadID: res.UploadId,
        Content: fs.createReadStream(filePath, {
          start: offset,
          end: offset + partSize - 1,
        }),
      });
      const eTag = uploadResult.ETag;
      console.log(`partNumber${partNumber} Etag:`, eTag);
      partsInfo.push(new UploadedPart(partNumber, eTag));
      partNumber++;
      offset += partSize;
    }
    console.log('parts information', partsInfo);

    
    const completeRes = await client.completeMultipartUpload({
      Bucket: bucketName,
      Key: objectName,
      UploadID: res.UploadId,
      Parts: partsInfo,
    });

    console.log('result status:', completeRes.StatusCode);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="0abcdb5b"></span>
### Set object metadata information using SetObjectMeta.

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
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Header:', error.headers);
    console.log('Response Err Code:', error.code);
    console.log('Response Err Msg:', error.message);
  } else {
    console.log('unexpected exception, message: ', error);
  }
}

async function main() {
  const meta: Record<string, string> = {};
  meta.key = 'value';
  try {
    const res = await client.setObjectMeta({
      Bucket: bucketName,
      Key: objectKey,
      
      Meta: meta,
      
      ContentType: 'text/html',
      
      ContentLanguage: 'zh-cn',
      
      CacheControl: 'no-store',
   
      Expires: new Date('2028/01/01'),
     
      ContentDisposition: 'example.png',
      
      ContentEncoding: 'deflate',
    });
    console.log('putObject Request ID:', res.RequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="ed2fb090"></span>
### Query Object Metadata Information (Determine Object Existence)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before obtaining object metadata, you must have the <code>tos:GetObject</code> permission. For specific instructions, refer to <a href="https://docs.byteplus.com/docs/tos/docs-overview_6">IAM Policy Overview</a>.</div>


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
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Header:', error.headers);
    console.log('Response Err Code:', error.code);
    console.log('Response Err Msg:', error.message);
  } else {
    console.log('unexpected exception, message: ', error);
  }
}

const bucketName = 'harmonyos-sdk-test-bucket';
const objectKey = 'example_dir/example.txt';
async function main() {
  try {
    const res = await client.headObject({
      Bucket: bucketName,
      Key: objectKey,
    });
    console.log('headObject Request ID:', res.RequestId);

    console.log('headObject Response ContentLanguage:', res.ContentLength);

    console.log('headObject Response ContentDisposition:', res.ContentDisposition);
 
    console.log('headObject Response ContentEncoding:', res.ContentEncoding);

    console.log('headObject Response CacheControl:', res.CacheControl);
 
    console.log('headObject Response ContentType:', res.ContentType);
  
    console.log('headObject Response Expires:', res.Expires);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="a2055d6c"></span>
## **Relevant Documentation**

For API documentation on setting object metadata, refer to [SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta).
