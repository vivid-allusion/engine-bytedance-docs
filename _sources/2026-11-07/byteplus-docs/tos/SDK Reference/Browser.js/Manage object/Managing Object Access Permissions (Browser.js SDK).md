---
title: "Managing Object Access Permissions (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-access-to-objects-browser-js-sdk"
---

This article describes how to obtain and configure access permissions for objects. Object access permissions take precedence over bucket access permissions. If object access permissions are not set, bucket access permissions will apply.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before configuring read and write permissions for an object, you must have the <code>tos:PutObjectACL</code> permission or the WRITE_ACP object ACL permission. For detailed information, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission configuration guide</a>.</div>


<span id=".YWNsLeivtOaYjg=="></span>
## ACL description

Object ACL permissions include the following types.


|Access permission |Description |Access permission value |
|---|---|---|
|READ |Allows the authorized user to read object data and metadata. |enum.PermissionRead |
|READ_ACP |Allow authorized users to read the object's ACL. |enum.PermissionReadAcp |
|WRITE_ACP |Authorized individuals are permitted to write ACLs for applicable objects. |enum.PermissionWriteAcp |
|FULL_CONTROL |Grants the authorized user READ, READ_ACP, and WRITE_ACP permissions on a object. |enum.PermissionFullControl |


You may specify detailed ACL permission information in the request body, or set access permissions in the request header.

<span id=".6K-35rGC5aS05Lit6K6-572u6K6_6Zeu5p2D6ZmQ"></span>
## Setting access permissions in the request header

The types of object read and write permissions that can be set via the x\-tos\-acl request header are as follows.


|Access permission |Description |Access permission value |
|---|---|---|
|Private |The owner of the object possesses full permissions, while other users do not have permission to operate the object. |private |
|Public Read |The owner of an object possesses all permissions, while other users have only read permission for that object. |public\-read |
|Public Read and Write |All users have read permission for this object. |public\-read\-write |
|Authenticated User Read Access |The owner of the object has all permissions, while authenticated users have read permission for the object. |authenticated\-read |
|Bucket Owner Read |The object owner has all permissions. The bucket owner has read permission for this object. |bucket\-owner\-read |
|Bucket Owner Full Control |Both the bucket owner and the object owner have full operation permissions on the object. |bucket\-owner\-full\-control |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".6K6-572u5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
### Configuring object read/write permissions

The following code sets the object's read and write permissions via the x\-tos\-acl header.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <button id="upload">Upload</button>
    <input id="file" type="file" />
    <script src="https://tos-public.volccdn.com/obj/volc-tos-public/@volcengine/tos-sdk@latest/browser/tos.umd.production.min.js"></script>
    <script type="text/javascript">
      const client = new TOS({
        region: yourRegion,
        endpoint: yourEndpoint,
        accessKeyId: yourAccessKey,
        accessKeySecret: yourSecretKey,
        stsToken: yourSecurityToken,
        bucket: bucketName,
      });
      const objectName = 'exampledir/putObjectobject.txt';

      const main = async () => {
        await client.putObjectAcl({
          bucket: bucketName,
          key: objectName,
          acl: 'public-read-write',
        });
      };

      main();
    </script>
  </body>
</html>
```


<span id=".6I635Y-W5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
### Obtaining read and write permissions for an object

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before obtaining access permissions for an object, you must have the <code>tos:GetObjectACL</code> permission or possess the object's ACL permission READ_ACP. For detailed instructions, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permission Configuration Guide</a>.</div>


The following code is used to obtain access permissions for an object.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Document</title>
  </head>
  <body>
    <button id="upload">Upload</button>
    <input id="file" type="file" />
    <script src="https://tos-public.volccdn.com/obj/volc-tos-public/@volcengine/tos-sdk@latest/browser/tos.umd.production.min.js"></script>
    <script src="./const.js"></script>
    <script type="text/javascript">
      const client = new TOS({
        region: yourRegion,
        endpoint: yourEndpoint,
        accessKeyId: yourAccessKey,
        accessKeySecret: yourSecretKey,
        stsToken: yourSecurityToken,
        bucket: bucketName,
      });
      const objectName = 'exampledir/putObjectobject.txt';

      const main = async () => {
        const { data: newData } = await client.getObjectAcl({
          bucket: bucketName,
          key: objectName,
        });
        console.log('object acl info:', newData);
      };

      main();
    </script>
  </body>
</html>
```
