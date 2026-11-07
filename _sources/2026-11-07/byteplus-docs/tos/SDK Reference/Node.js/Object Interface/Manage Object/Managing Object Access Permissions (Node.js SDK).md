---
title: "Managing Object Access Permissions (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/managing-object-access-node-js-sdk"
---

This article describes how to obtain and set access permissions for objects. The access rights of an object take precedence over the access rights of the bucket, and if the object has no access rights set, the access rights of the bucket are followed.

<span id="a43f4f8b"></span>
## **Set the read and write permissions of the object**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must have <code>tos: PutObjectACL</code>permission or WRITE_ACP object ACL permission before setting the object read and write permissions, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


<span id=".YWNsLeivtOaYjg=="></span>
### ACL Description

Object ACL permissions include the following types.


|access rights |describe |access permission value |
|---|---|---|
|READ |Allows authorized persons to read object data and its metadata |PermissionType.PermissionRead |
|READ_ACP |Allows authorized persons to read the object ACL |PermissionType.PermissionReadAcp |
|WRITE_ACP |Allows authorized parties to write ACLs for applicable objects |PermissionType.PermissionWriteAcp |
|FULL_CONTROL |Allows authorized READ, READ_ACP, and WRITE_ACP permissions on objects |PermissionType.PermissionFullControl |


You can fill in detailed ACL permission information in the request body, or set access permissions in the request header.

<span id="38143fa3"></span>
### **Fill in the detailed ACL permission information in the request body**

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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    // The specified objectKey.
    const objectKey = '*** Provide your object key ***';

    // Set object ACL.
    const { requestId } = await client.putObjectAcl({
      bucket: bucketName,
      key: objectKey,
      // If versioning is enabled for the bucket, you can specify a particular version by setting the versionId.
      versionId: '',
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
            Permission: PermissionType.PermissionRead,
          },
        ],
      },
    });
    console.log('putObjectAcl Request ID:', requestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".6K-35rGC5aS05Lit6K6-572u6K6_6Zeu5p2D6ZmQ"></span>
### Set access permissions in the request header

The read and write permissions of the object set by the x\-tos\-acl request header include the following types.


|access rights |describe |access permission value |
|---|---|---|
|private |The owner of the object has all permissions, and no other user has permission to operate on the object. |private |
|public reading |The owner of the object has all permissions, other users only have read permissions to the object. |public\-read |
|public reading and writing |All users have read access to the object. |public\-read\-write |
|authenticated user read |The owner of the object has all permissions, and the authenticated user has read access to the object. |authenticated\-read |
|Bucket owner read |The object owner has all permissions, and the bucket owner has read permissions on this object. |bucket\-owner\-read |
|The bucket owner has all permissions |Both the bucket owner and the object owner have all the operating rights on the object. |bucket\-owner\-full\-control |


The following code sets the read and write permissions of an object via x\-tos\-acl.

```javascript
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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    // The specified objectKey.
    const objectKey = '*** Provide your object key ***';

    // Set object ACL
    const { requestId } = await client.putObjectAcl({
      bucket: bucketName,
      key: objectKey,
      // If the bucket has versioning enabled, you can specify a specific version by setting the versionId.
      // versionId: '',
      acl: ACLType.ACLPublicRead,
    });
    console.log('putObjectAcl Request ID:', requestId);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="ac5742fe"></span>
### **Related documentation**

For the API documentation on setting read and write permissions for objects, see [PutObjectACL](https://docs.byteplus.com/docs/tos/reference-putobjectacl).

<span id=".6I635Y-W5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
## Gets read and write permissions for an object

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You must have the <code>tos: GetObjectACL</code>permission or READ_ACP ACL permission for the object before you can gain access to the object, see <a href="https://docs.byteplus.com/docs/tos/docs--overview">Overview</a>.</div>


The following code is used to obtain access to an object.

```javascript
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

async function main() {
  try {
    const bucketName = 'node-sdk-test-bucket';
    // The specified objectKey
    const objectKey = '*** Provide your object key ***';

    // Set object ACL
    const { data, requestId } = await client.getObjectAcl({
      bucket: bucketName,
      key: objectKey,
      // If versioning is enabled for the bucket, you can specify a particular version by setting the versionId.
      // versionId: '',
    });
    console.log('getObjectAcl Request ID:', requestId);

    // Get object Owner information
    console.log('GetObjectACL Owner: %o', data.Owner);
    for (const grant of data.Grants) {
      // Permissions held by the grantee
      console.log('Grant Permission:', grant.Permission);
      // Type of the grantee
      console.log('Grant GranteeV2 Type', grant.Grantee.Type);
      // When Type is CanonicalUser, it represents the ID of the grantee
      console.log('Grant GranteeV2 ID', grant.Grantee.ID);
      // Name of the grantee
      console.log('Grant GranteeV2 DisplayName', grant.Grantee.DisplayName);
      // Authorized user group
      console.log('Grant GranteeV2 Canned', grant.Grantee.Canned);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="381bccf6"></span>
### **Related documentation**

For the API documentation on obtaining read and write permissions for objects, see [GetObjectACL](https://docs.byteplus.com/docs/tos/reference-getobjectacl).
