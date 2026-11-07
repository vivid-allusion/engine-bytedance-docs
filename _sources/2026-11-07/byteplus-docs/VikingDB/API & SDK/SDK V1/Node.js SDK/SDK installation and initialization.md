---
title: "SDK installation and initialization"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/nodesdk_SDK_installation_and_initialization"
---

<span id="sdk-installation-and-initialization"></span>
# SDK installation and initialization

To start using VikingDB in your Node.js applications, you first need to install and initialize the SDK. This guide provides the necessary commands and code examples to configure your access credentials and establish a client connection, enabling you to begin performing database operations.

<span id="8fc8ad40"></span>
# Prerequisites


1. You have [registered an account and enabled the related service](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

2. You have obtained the access key for BytePlus. The access key consists of an access key ID and a secret access key. You can log in to the BytePlus console and go to the Key management page to view the access key ID and secret access key of the current account. For more information, refer to [Access key management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).


<span id="d60638ff"></span>
# Install the SDK

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use pnpm to manage dependencies and install Node 12 or later.</div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To achieve accurate type inference, we strongly recommend that you use TypeScript for development. The SDK provides complete type definitions and autocompletion. All the following demos are written in TypeScript.</div>


```TypeScript
$ # Install SDK V1.19.0 or later. 
$ pnpm add @volcengine/openapi
```


<span id="75a8f798"></span>
# Initialize the SDK

Configure the access key and initialize the client based on the vector database name and tokens. The domain name (specified by the host parameter) supports both HTTP and HTTPS protocols. You can choose either of them as needed.


* Domain name for Hong Kong: [api-vikingdb.mlp.cn-hongkong.bytepluses.com](http://api-vikingdb.mlp.cn-hongkong.bytepluses.com/)

* Domain name for Johor: api\-vikingdb.mlp.ap\-mya.byteplus.com

* If you access VikingDB on a private network, you can configure and obtain the domain name by referring to [Access VikingDB on a private network](https://www.volcengine.com/docs/84313/1254445). Currently, private network access supports only the HTTP protocol.


You can configure the region parameter as required, such as `cn-hongkong` for Hong Kong and `ap-southeast-1` for Johor.

In the sample code, replace `Your ak` with your access key ID, replace `Your sk` with your secret access key, and replace `Your region` with the domain name and region that you use.

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

const vikingdbService = new vikingdb.VikingdbService({ 
  ak: 'Your ak', 
  sk: 'Your sk', 
  region: 'Your region', 
})
```


<span id="19fae697"></span>
## Requests with an assumed role

To make a request with an assumed role, you must first use `AssumeRole` to obtain a temporary access key ID, secret access key, and session token. For more information about `AssumeRole`, refer to the `AssumeRole` API documentation.

```TypeScript
import { sts, vikingdb } from '@volcengine/openapi' 

const stsService = new sts.StsService({ 
  RoleTrn: 'trn:iam::{accountId}:role/{roleName}', 
  RoleSessionName: 'TempSessionName', 
}) 

const { Result } = await stsService.AssumeRole() 

if (!Result.Credentials) { 
  return 
} 

const vikingdbService = new vikingdb.VikingdbService({ 
  ak: Result.Credentials.AccessKeyId, 
  sk: Result.Credentials.SecretAccessKey, 
  sessionToken: Result.Credentials.SessionToken 
})
```


<span id="2b33c55b"></span>
# Other instructions

<span id="496c9d45"></span>
## Type

The SDK provides complete type definitions, with all vector database elements organized under the `vikingdb` namespace. Some public types, such as `vikingdb.FieldType`, are placed directly under the `vikingdb` namespace. Module\-specific types, such as `vikingdb.collection.CreateCollectionRequest`, `vikingdb.index.IndexType`, and `vikingdb.search.SearchResponse`, are placed under their respective namespaces.

<span id="37c9b844"></span>
## Response

All SDK responses are instances of `VikingdbResponse`. The caller can use the `OriginalRequest` and `Logid` fields to obtain the original request body and request log ID.

For an SDK internal error that occurs before a request is sent, the SDK throws `VikingdbError`, which contains the `Code` and `Message` fields to provide the error code and error message. For an API error, the SDK throws `VikingdbRequestError`, which inherits from `VikingdbError` and contains the `OriginalRequest` and `Logid` fields.

```TypeScript
import { vikingdb } from '@volcengine/openapi' 

declare const service: vikingdb.VikingdbService // Replace it with the instance that you have initialized. 

try { 
  const response = await service.collection.CreateCollection({ 
    CollectionName: 'test_collection_1', 
    Description: 'collection_description', // optional 
    CollectionAliases: ['collection_alias_1', 'collection_alias_2'], // optional 
    Fields: [ 
      { FieldName: 'Id', FieldType: vikingdb.FieldType.Int64, IsPrimary: true }, // primary key 
      { FieldName: 'Name', FieldType: vikingdb.FieldType.String, DefaultValue: 'Hello world'/* optional */ }, // scalar field 
      { FieldName: 'DenseVector', FieldType: vikingdb.FieldType.DenseVector, Dim: 4 }, // dense vector field 
      { FieldName: 'SparseVector', FieldType: vikingdb.FieldType.SparseVector }, // sparse vector field 
      { FieldName: 'Text', FieldType: vikingdb.FieldType.Text, PipelineName: 'text_bge_m3', /* optional */ }, // text field 
    ] 
  }) 
  console.log(response.OriginalRequest) // API request body 
  console.log(response.Logid) // request log ID 
} catch(e) { 
  if (e instanceof vikingdb.VikingdbRequestError) { 
    // request error 
    console.log(e.Code) // backend error code 
    console.log(e.Message) // backend error message 
    console.log(e.OriginalRequest) // API request body 
    console.log(e.Logid) // request log ID 
  } else if (e instanceof vikingdb.VikingdbError) { 
    console.log(e.Code) // SDK error code 
    console.log(e.Message) // SDK error message 
  } 
}
```


<span id="a4a71da7"></span>
## Precision

Due to the precision limitation of JavaScript, the SDK may lose precision when handling `int64` and `float32` data types.
