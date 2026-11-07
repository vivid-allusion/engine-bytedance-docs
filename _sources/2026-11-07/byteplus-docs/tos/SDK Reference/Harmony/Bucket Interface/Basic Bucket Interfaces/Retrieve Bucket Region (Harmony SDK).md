---
title: "Retrieve Bucket Region (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-region-harmony-sdk"
---

A Bucket is the globally unique namespace in TOS, functioning as a container for data and used to store Object data. This document describes how to obtain the region of a bucket.

<span id="2ec331fb"></span>
## Precautions


* By default, only the bucket owner can view the region where the bucket is located.

* When managing buckets and objects within buckets using the TOS Harmony SDK, you must use the domain name corresponding to the bucket's region. For more information about regions and access domain names, see [Regions and Access Domain Names](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).


<span id="4f0a7e17"></span>
## Sample Code

```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
  securityToken: 'Provide your securityToken',
  region: "Provide your region",
  endpoint: "Provide your endpoint",
});

function handleError(error: Error) {
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

const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {
  try {
    const res = await client.getBucketLocation({ Bucket: bucketName });

    console.log('Bucket Region:', res.Region);
  
    console.log('Bucket ExtranetEndpoint:', res.ExtranetEndpoint);

    console.log('Bucket IntranetEndpoint:', res.IntranetEndpoint);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="688d704c"></span>
## Relevant Documentation

For API documentation on retrieving the bucket region, refer to [GetBucketLocation](https://docs.byteplus.com/docs/tos/reference-getbucketlocation).
