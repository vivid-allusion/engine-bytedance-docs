---
title: "Deleting Objects (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-objects-net-sdk"
---

When an object is no longer in use, you may delete it to reduce cost overhead. Currently, the TOS .NET SDK supports deleting individual objects or specified multiple objects within a bucket. For buckets with versioning enabled, you can specify which version of an object to delete.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Before deleting an object, you must ensure that your account has the tos:DeleteObject permission. For detailed instructions, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To delete a specified version of an object in a bucket with versioning enabled, you must have the tos:DeleteObjectVersion permission. For specific operations, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5Yig6Zmk5oyH5a6a5a-56LGh"></span>
### Delete Specified Object

The following code is used to delete the specified object.

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
                var deleteObjectInput = new DeleteObjectInput()
                {
                    Bucket = bucketName,
                    Key = objectKey
                };

                var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                Console.WriteLine("DeleteObject succeeded, Request ID {0}", deleteObjectOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("DeleteObject failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("DeleteObject failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("DeleteObject failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("DeleteObject failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("DeleteObject failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("DeleteObject failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5Yig6Zmk5oyH5a6a54mI5pys55qE5a-56LGh"></span>
### Delete the object of the specified version

The following code is used to delete an object of a specified version.

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
            var versionID = "*** Provide object Version ID";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var deleteObjectInput = new DeleteObjectInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    VersionID = versionID
                };

                var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                Console.WriteLine("DeleteObject succeeded, Request ID {0}", deleteObjectOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("DeleteObject failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("DeleteObject failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("DeleteObject failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("DeleteObject failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("DeleteObject failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("DeleteObject failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5om56YeP5Yig6Zmk5a-56LGh"></span>
### Batch Deletion of Objects

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">In a versioned bucket, when the DeleteMultiObjects API is called to delete objects in bulk, if <code>versionId</code> is not specified in the Delete request, a delete marker will be inserted. If <code>versionId</code> is specified, the specified version of the object will be permanently deleted.</div>


* <div data-tips="true" data-tips-type="warning">The response mode supported for batch object deletion can be configured using <code>quiet</code>. If <code>quiet</code> is set to <code>false</code>, the response will include the deletion result for each object, regardless of whether the deletion was successful. If <code>quiet</code> is set to <code>true</code>, the response will only include results for objects whose deletion failed; objects not listed in the response are considered successfully deleted.</div>



The following code is used for batch deletion of objects.

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
            var objectKey1 = "*** Provide Object Key ***";
            var objectKey2 = "*** Provide Object Key ***";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var objects = new[]
                {
                    new ObjectTobeDeleted() { Key = objectKey1 },
                    new ObjectTobeDeleted() { Key = objectKey2 },
                };
                var deleteMultiObjectsInput = new DeleteMultiObjectsInput()
                {
                    Bucket = bucketName,
                    Objects = objects,
                };

                var deleteMultiObjectsOutput = client.DeleteMultiObjects(deleteMultiObjectsInput);
                Console.WriteLine("DeleteMultiObjects succeeded, Request ID {0}", deleteMultiObjectsOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("DeleteMultiObjects failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("DeleteMultiObjects failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("DeleteMultiObjects failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("DeleteMultiObjects failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("DeleteMultiObjects failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("DeleteMultiObjects failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5om56YeP5Yig6Zmk5oyH5a6a54mI5pys55qE5a-56LGh"></span>
### Bulk Deletion of Objects of a Specified Version

The following code is used to delete multiple object data from a storage bucket based on specified object names and version numbers.

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
            var objectKey1 = "*** Provide Object Key ***";
            var objectKey2 = "*** Provide Object Key ***";
            var versionID1 = "*** Provide objectKey1 Version ID ***";
            var versionID2 = "*** Provide objectKey2 Version ID ***";
            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var objects = new[]
                {
                    new ObjectTobeDeleted() { Key = objectKey1, VersionID = versionID1 },
                    new ObjectTobeDeleted() { Key = objectKey2, VersionID = versionID2 },
                };
                var deleteMultiObjectsInput = new DeleteMultiObjectsInput()
                {
                    Bucket = bucketName,
                    Objects = objects,
                };

                var deleteMultiObjectsOutput = client.DeleteMultiObjects(deleteMultiObjectsInput);
                Console.WriteLine("DeleteMultiObjects succeeded, Request ID {0}", deleteMultiObjectsOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("DeleteMultiObjects failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("DeleteMultiObjects failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("DeleteMultiObjects failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("DeleteMultiObjects failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("DeleteMultiObjects failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("DeleteMultiObjects failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5Yig6Zmk5qG25Lit5omA5pyJ5a-56LGh"></span>
### Delete all objects in the bucket

The following code is used to delete all objects in the storage bucket.

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
                var keyMarker = "";
                var isTruncated = true;

                while (isTruncated)
                {
                    var listObjectVersionsInput = new ListObjectVersionsInput()
                    {
                        Bucket = bucketName,
                        KeyMarker = keyMarker,
                    };
                    var listObjectVersionsOutput = client.ListObjectVersions(listObjectVersionsInput);

                    foreach (var obj in listObjectVersionsOutput.Versions)
                    {
                        var deleteObjectInput = new DeleteObjectInput()
                        {
                            Bucket = bucketName,
                            Key = obj.Key,
                            VersionID = obj.VersionID
                        };
                        var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                        Console.WriteLine("Delete {0}, Request ID {1}", obj.Key, deleteObjectOutput.RequestID);
                    }

                    foreach (var deleteMarker in listObjectVersionsOutput.DeleteMarkers)
                    {
                        var deleteObjectInput = new DeleteObjectInput()
                        {
                            Bucket = bucketName,
                            Key = deleteMarker.Key,
                            VersionID = deleteMarker.VersionID
                        };
                        var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                        Console.WriteLine("Delete {0}, Request ID {1}", deleteMarker.Key, deleteObjectOutput.RequestID);
                    }

                    isTruncated = listObjectVersionsOutput.IsTruncated;
                    keyMarker = listObjectVersionsOutput.NextKeyMarker;
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("Clear Bucket failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("Clear Bucket failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("Clear Bucket failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("Clear Bucket failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Clear Bucket failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Clear Bucket failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to the API for deleting objects, see [DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject).
