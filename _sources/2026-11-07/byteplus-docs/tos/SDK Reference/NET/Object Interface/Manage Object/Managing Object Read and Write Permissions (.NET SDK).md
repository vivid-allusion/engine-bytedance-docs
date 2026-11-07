---
title: "Managing Object Read and Write Permissions (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-read-and-write-permissions-net-sdk"
---

This article describes how to obtain and configure access permissions for objects. The access permissions of an object take precedence over those of the bucket. If no access permissions are set for the object, the bucket's access permissions apply.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

Before setting object read/write permissions, you must ensure that your account has the `tos:PutObjectACL` permission or the WRITE_ACP object ACL permission. For specific operations, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

<span id=".6K6-572u5a-56LGh55qELWFjbC3mnYPpmZDkv6Hmga8="></span>
## Set the object's ACL information.

You can set detailed ACL permission information in either the request body or the request header. Object ACL permissions include the following types.


|**Access permission** |**Description** |**Access Permission Value** |
|---|---|---|
|READ |Allows the authorized user to read object data and metadata. |*PermissionType.PermissionRead* |
|READ_ACP |Allows the grantees to read the object ACL. |*PermissionType.PermissionReadAcp* |
|WRITE_ACP |Authorized users are permitted to write ACLs for applicable objects. |*PermissionType.PermissionWriteAcp* |
|FULL_CONTROL |Grants the authorized user READ, READ_ACP, and WRITE_ACP permissions on a object. |*PermissionType.PermissionFullControl* |


The following code is used to set detailed ACL permissions for an object in the request body.

```C#
using System;
using TOS;
using TOS.Error;
using TOS.Model;

namespace ConsoleApp
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var ak = Environment.GetEnvironmentVariable("TOS_ACCESS_KEY");
            var sk = Environment.GetEnvironmentVariable("TOS_SECRET_KEY");
            var endpoint = "your endpoint";
            var region = "your region";
            var bucketName = "*** Provide your bucket name ***";
            var objectKey = "*** Provide your object key ***";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var putObjectACLInput = new PutObjectACLInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    VersionID = "",
                    Owner = new Owner()
                    {
                        ID = "ownerId"
                    },
                    Grants = new[]
                    {
                        new Grant()
                        {
                            Grantee = new Grantee()
                            {
                                ID = "userId",
                                Type = GranteeType.GranteeUser,
                            },
                            Permission = PermissionType.PermissionRead
                        }
                    }
                };

                var putObjectAclOutput = client.PutObjectACL(putObjectACLInput);
                Console.WriteLine("PutObjectACL succeeded, Request ID {0}", putObjectAclOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("PutObjectACL failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("PutObjectACL failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("PutObjectACL failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("PutObjectACL failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("PutObjectACL failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("PutObjectACL failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".6K6-572u5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
## Configuring Object Read and Write Permissions

There are six categories of object read/write permissions that can be set via the x\-tos\-acl request header.


|**Access permission** |**Description** |Access Permission Value |
|---|---|---|
|Private |Private. The owner of the object possesses all permissions, while other users are not authorized to operate the object. |*ACLType.ACLPrivate* |
|Public Read |Public reading. The owner of an object possesses all permissions, while other users have only read permission for that object. |*ACLType.ACLPublicRead* |
|Public Read and Write |Public read and write access. All users have read permission for this object. |*ACLType.ACLPublicReadWrite* |
|Read by Certified User |The owner of the object possesses all permissions, while authenticated users are granted read permission for the object. |*ACLType.ACLAuthRead* |
|Bucket Owner Read |The object owner has full permissions, while the bucket owner has read permission for this object. |*ACLType.ACLBucketOwnerRead* |
|The bucket owner possesses all permissions. |Both the bucket owner and the object owner have all operation permissions on the object. |*ACLType.ACLBucketOwnerFullControl* |


The following code sets the object's read and write permissions via the x\-tos\-acl request header.

```C#
using System;
using TOS;
using TOS.Error;
using TOS.Model;

namespace ConsoleApp
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var ak = Environment.GetEnvironmentVariable("TOS_ACCESS_KEY");
            var sk = Environment.GetEnvironmentVariable("TOS_SECRET_KEY");
            var endpoint = "your endpoint";
            var region = "your region";
            var bucketName = "*** Provide your bucket name ***";
            var objectKey = "*** Provide your object key ***";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var putObjectACLInput = new PutObjectACLInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    VersionID = "",
                    ACL = ACLType.ACLPrivate,
                };

                var putObjectAclOutput = client.PutObjectACL(putObjectACLInput);
                Console.WriteLine("PutObjectACL succeeded, Request ID {0}", putObjectAclOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("PutObjectACL failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("PutObjectACL failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("PutObjectACL failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("PutObjectACL failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("PutObjectACL failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("PutObjectACL failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".6I635Y-W5a-56LGh55qE6K-75YaZ5p2D6ZmQ"></span>
## Obtain Read and Write Permissions for an Object

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before obtaining access to an object, ensure that your current account has the <code>tos:GetObjectACL</code> permission or the object's ACL permission READ_ACP. For detailed instructions, refer to the <a href="https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide">Permissions Configuration Guide</a>.</div>


The following code is used to obtain read and write permissions for the object.

```C#
using System;
using TOS;
using TOS.Error;
using TOS.Model;

namespace ConsoleApp
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var ak = Environment.GetEnvironmentVariable("TOS_ACCESS_KEY");
            var sk = Environment.GetEnvironmentVariable("TOS_SECRET_KEY");
            var endpoint = "your endpoint";
            var region = "your region";
            var bucketName = "*** Provide your bucket name ***";
            var objectKey = "*** Provide your object key ***";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var getObjectACLInput = new GetObjectACLInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                };

                var getObjectAclOutput = client.GetObjectACL(getObjectACLInput);
                Console.WriteLine("GetObjectACL succeeded, Request ID {0}", getObjectAclOutput.RequestID);
 
                foreach (var grant in getObjectAclOutput.Grants)
                {
                    Console.WriteLine("Grant Permission {0}", grant.Permission);
                    Console.WriteLine("Grant Grantee ID {0}", grant.Grantee.ID);
                    Console.WriteLine("Grant Grantee DisplayName {0}", grant.Grantee.DisplayName);
                    Console.WriteLine("Grant Grantee Canned {0}", grant.Grantee.Canned);
                    Console.WriteLine("Grant Grantee Type {0}", grant.Grantee.Type);
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("GetObjectACL failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("GetObjectACL failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("GetObjectACL failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("GetObjectACL failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("GetObjectACL failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("GetObjectACL failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* For a detailed introduction to the API for configuring object read and write permissions, see [PutObjectAcl](https://docs.byteplus.com/docs/tos/reference-putobjectacl).

* For a detailed introduction to the API interface for obtaining object read and write permissions, see [GetObjectAcl](https://docs.byteplus.com/docs/tos/reference-getobjectacl).
