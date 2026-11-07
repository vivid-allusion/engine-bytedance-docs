---
title: "Managing Mirror Origin Retrieval (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-mirror-backsource-harmony-sdk"
---

Mirror back\-to\-origin is mainly used in scenarios where seamless data migration to TOS is required. For example, if your web service is already running on a self\-built origin server and you migrate static web pages to TOS for storage, you can configure mirror back\-to\-origin rules to retrieve the part of data that has not yet been migrated to TOS.

<span id="ffe723f1"></span>
## Sample Code

<span id="20b81753"></span>
### **Configure Origin Fetch**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A bucket supports the creation of only one origin retrieval rule.</div>


* <div data-tips="true" data-tips-type="warning">Mirror back\-to\-origin supports objects up to a maximum size of 5 GiB.</div>


* <div data-tips="true" data-tips-type="warning">Redirect to origin supports a maximum of 300 GiB.</div>



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

const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {

async function main() {
  try {
    const mirrorRule: MirrorBackRule = {
  
      ID: 'rule1',
      Condition: {
  
        HttpCode: 404,
      },
      Redirect: {
    
        RedirectType: RedirectType.RedirectTypeMirror,
    
        FetchSourceOnRedirect: true,
      
        PassQuery: true,
   
        FollowRedirect: true,
        MirrorHeader: {
    
          PassAll: false,
     
          Pass: ['header-1', 'header-2'],
      
          Remove: ['header-3', 'header-4'],
        },
   
        PublicSource: {
          SourceEndpoint: {
            Primary: ['https://www.example.com'],
          },
        },
      },
    };
    const res = await client.putBucketMirrorBack({
      Bucket: bucketName,
      Rules: [mirrorRule],
    });
    console.log('putBucketMirrorBack Request ID: ', res.RequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="ad36d5e4"></span>
### **Fetch Mirror from Origin**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must be the owner of the bucket to access its mirror back\-to\-origin rules.</div>


```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak", 
  accessKeySecret: "Provide your sk", 
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
const bucketName = 'harmonyos-sdk-test-bucket';
async function main() {
  try {
    const res = await client.getBucketMirrorBack({
      Bucket: bucketName,
    });
    console.log('getBucketMirrorBack Request ID: ', res.RequestId);
    console.log('getBucketMirrorBack Rules Length: ', res.Rules.length);
    for (const rule of res.Rules) {
      
      console.log('rule ID:', rule.ID);
      
      console.log('rule Condition HttpCode:', rule.Condition.HttpCode);
      
      console.log('rule Redirect RedirectType:', rule.Redirect.RedirectType);
      
      console.log('rule Redirect FetchSourceOnRedirect:', rule.Redirect.FetchSourceOnRedirect);
      
      console.log('rule Redirect PassQuery:', rule.Redirect.PassQuery);
      
      console.log('rule Redirect FollowRedirect:', rule.Redirect.FollowRedirect);
     
      console.log('rule Redirect MirrorHeader PassAll:', rule.Redirect.MirrorHeader?.PassAll);
     
      console.log('rule Redirect MirrorHeader Pass:', rule.Redirect.MirrorHeader?.Pass);
  
      console.log('rule Redirect MirrorHeader Remove:', rule.Redirect.MirrorHeader?.Remove);
   
      console.log('rule Redirect PublicSource SourceEndpoint:', rule.Redirect.PublicSource?.SourceEndpoint);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="81e5287a"></span>
### **Delete Mirror Origin Retrieval**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must be the owner of the bucket to delete its mirror source retrieval rule.</div>


```TypeScript
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos_harmonyos_sdk';


const client = new TosClient({
  accessKeyId: "Provide your ak",
  accessKeySecret: "Provide your ak",
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
    const res = await client.deleteBucketMirrorBack({
      Bucket: bucketName,
    });
    console.log('deleteBucketMirrorBack Request ID: ', res.RequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="7f230877"></span>
## **Relevant Documentation**

For more information about origin fetch, see [Setting Origin Rules](https://docs.byteplus.com/docs/tos/Overview9).
