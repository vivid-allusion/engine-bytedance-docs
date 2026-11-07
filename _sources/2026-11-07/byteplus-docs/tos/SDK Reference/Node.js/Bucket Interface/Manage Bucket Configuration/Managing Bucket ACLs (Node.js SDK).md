---
title: "Managing Bucket ACLs (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-acl-node-js-sdk"
---

You can set the bucket ACL through the interface provided by the TOS SDK. Permissions can be set through the request header and request body.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisite**


* The account that configures the bucket ACL must be the creator of the bucket or have write access to the bucket ACL.

* Only ACL configuration for the main account ID is supported, and sub\-accounts are not supported.


<span id=".5qG2LWFjbC3or7TmmI4="></span>
## Bucket ACL Description


|**access rights** |**describe** |**enumeration type** |
|---|---|---|
|READ |Allows authorized parties to list objects in buckets for sharding tasks. |PermissionType\*.\*PermissionRead |
|WRITE |Allows authorized parties to create, overwrite, and delete arbitrary objects in the bucket, initialize sharding tasks, upload sharding, merge sharding, and cancel sharding tasks. |PermissionType.PermissionWrite |
|READ_ACP |Allows authorized parties to read the bucket ACL. |PermissionType.PermissionReadAcp |
|WRITE_ACP |Allows authorized parties to set ACLs for applicable buckets. |PermissionType.PermissionWriteAcp |
|FULL_CONTROL |Allows authorized persons to have READ, WRITE, READ_ACP and WRITE_ACP permissions on the bucket. |PermissionType.PermissionFullControl |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".6YCa6L-H6K-35rGC5L2T6K6-572uLWFjbC3mnYPpmZA="></span>
### **Set ACL permissions through request body**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before setting ACL permissions for buckets, you must have <code>tos: PutBucketACL</code>permissions, or <code>WRITE_ACP</code>bucket ACL permissions. For specific operations, please refer to <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError, GranteeType, PermissionType } from '@volcengine/tos-sdk';

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
    const { requestId: putAclRequestId } = await client.putBucketAcl({
      bucket: bucketName,
      aclBody: {
        Owner: {
          // Get Bucket Owner ID
          ID: 'ownerid',
        },
        Grants: [
          {
            Grantee: {
              ID: 'userId',
              Type: GranteeType.GranteeUser,
            },
            Permission: PermissionType.PermissionWrite,
          },
        ],
      },
    });
    console.log('putBucketAcl Request ID: ', putAclRequestId);

    const { data, requestId: getAclRequestId } = await client.getBucketAcl(bucketName);
    console.log('getBucketAcl Request ID: ', getAclRequestId);
    console.log('getBucketAcl Owner:', data.Owner);
    for (const grant of data.Grants) {
      // The permissions that the grantee has for the bucket
      console.log('Grant Permission:', grant.Permission);
      // When the Type is CanonicalUser, it represents the ID of the grantee
      console.log('Grant Grantee ID', grant.Grantee.ID);
      // The name of the grantee to whom the permission is granted
      console.log('Grant Grantee DisplayName', grant.Grantee.DisplayName);
      // The authorized user group
      console.log('Grant Grantee Canned', grant.Grantee.Canned);
      // The type of the grantor
      console.log('Grant Grantee Type', grant.Grantee.Type);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6YCa6L-H6K-35rGC5aS06K6-572u5p2D6ZmQ"></span>
### **Set permissions via request headers**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before setting ACL permissions for buckets, you must have <code>tos: PutBucketACL</code>permissions, or <code>WRITE_ACP</code>bucket ACL permissions. For specific operations, please refer to <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError, ACLType } from '@volcengine/tos-sdk';

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
    const { requestId: putAclRequestId } = await client.putBucketAcl({
      bucket: bucketName,
      acl: ACLType.ACLPrivate,
    });
    console.log('putBucketAcl Request ID: ', putAclRequestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6I635Y-W5a2Y5YKo5qG25p2D6ZmQ"></span>
### **Get bucket permissions**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before you can gain access to a bucket, you must have <code>tos: GetBucketACL</code>permission, or <code>READ_ACP</code>bucket ACL permission. For specific operations, please refer to <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


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
    const { data, requestId: getAclRequestId } = await client.getBucketAcl(bucketName);
    console.log('getBucketAcl Request ID: ', getAclRequestId);
    console.log('getBucketAcl Owner:', data.Owner);
    for (const grant of data.Grants) {
      // The permissions that the grantee has for the bucket
      console.log('Grant Permission:', grant.Permission);
      // When Type is CanonicalUser, it represents the ID of the grantee
      console.log('Grant Grantee ID', grant.Grantee.ID);
      // The name of the grantee to whom the permission is granted
      console.log('Grant Grantee DisplayName', grant.Grantee.DisplayName);
      // The authorized user group
      console.log('Grant Grantee Canned', grant.Grantee.Canned);
      // The type of the grantor
      console.log('Grant Grantee Type', grant.Grantee.Type);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related documentation**

To manage the permissions of buckets, see [Bucket ACLs](https://docs.byteplus.com/docs/tos/docs-bucket-acls).
