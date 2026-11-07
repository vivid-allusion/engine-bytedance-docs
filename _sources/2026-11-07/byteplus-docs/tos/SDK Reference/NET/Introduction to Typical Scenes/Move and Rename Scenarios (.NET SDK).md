---
title: "Move and Rename Scenarios (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Move-and-rename-scenes-net-sdk"
---

If you need to rename a file within a Bucket, you can use the CopyObject interface to copy the source object to the target object, and then use the DeleteObject interface to remove the source object.

<span id=".6YeN5ZG95ZCN5Y2V5Liq5a-56LGh"></span>
## Rename a single object

The following code is used to rename the object src\-object to dest\-object within the storage bucket.

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
            var srcObjectKey = "src-object";
            var dstObjectKey = "dest-object";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var copyObjectInput = new CopyObjectInput()
                {
                    Bucket = bucketName,
                    Key = dstObjectKey,
                    SrcBucket = bucketName,
                    SrcKey = srcObjectKey,
                };
                var copyObjectOutput = client.CopyObject(copyObjectInput);
                Console.WriteLine("CopyObject succeeded, request id {0}", copyObjectOutput.RequestID);

                var deleteObjectInput = new DeleteObjectInput()
                {
                    Bucket = bucketName,
                    Key = srcObjectKey
                };
                var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                Console.WriteLine("DeleteObject succeeded, request id {0}", deleteObjectOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("CopyObject failed, request id {0}", ex.RequestID);
                Console.WriteLine("CopyObject failed, status code {0}", ex.StatusCode);
                Console.WriteLine("CopyObject failed, response error code {0}", ex.Code);
                Console.WriteLine("CopyObject failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("CopyObject failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("CopyObject failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".6YeN5ZG95ZCN55uu5b2V"></span>
## Rename Directory

The following code is used to rename the `exampledir1/` directory in the storage bucket to `exampledir2/`.

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
            var oldPrefix = "exampledir1/";
            var newPrefix = "exampledir2/";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var truncated = true;
                var marker = "";

                while (truncated)
                {
                    var listObjectsInput = new ListObjectsInput()
                    {
                        Bucket = bucketName,
                        MaxKeys = 1000,
                        Marker = marker,
                        Prefix = oldPrefix
                    };
                    var listObjectsOutput = client.ListObjects(listObjectsInput);

                    foreach (var obj in listObjectsOutput.Contents)
                    {
                        var newKey = newPrefix + obj.Key.Substring(oldPrefix.Length);
                        var copyObjectInput = new CopyObjectInput()
                        {
                            Bucket = bucketName,
                            Key = newKey,
                            SrcBucket = bucketName,
                            SrcKey = obj.Key
                        };
                        var copyObjectOutput = client.CopyObject(copyObjectInput);
                        Console.WriteLine("CopyObject succeeded, request id {0}", copyObjectOutput.RequestID);

                        var deleteObjectInput = new DeleteObjectInput()
                        {
                            Bucket = bucketName,
                            Key = obj.Key
                        };
                        var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                        Console.WriteLine("DeleteObject succeeded, request id {0}", deleteObjectOutput.RequestID);
                    }

                    truncated = listObjectsOutput.IsTruncated;
                    marker = listObjectsOutput.NextMarker;
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("CopyObject failed, request id {0}", ex.RequestID);
                Console.WriteLine("CopyObject failed, status code {0}", ex.StatusCode);
                Console.WriteLine("CopyObject failed, response header {0}", ex.Header);
                Console.WriteLine("CopyObject failed, response error code {0}", ex.Code);
                Console.WriteLine("CopyObject failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("CopyObject failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("CopyObject failed, {0}", ex.Message);
            }
        }
    }
}
```
