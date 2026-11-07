---
title: "Manage Object Tags (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-labels-net-sdk"
---

TOS supports object tagging and tag\-based object lifecycle management. This article describes how to manage object tags.

<span id="e8c298ce"></span>
## Notes


* To set object tags, you must have the `tos:PutObjectTagging` permission. For specific instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To retrieve object tags, you must have the `tos:GetObjectTagging` permission. For detailed instructions, see the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To delete object tags, you must have the `tos:DeleteObjectTagging` permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* Up to 10 tags can be added to each object, and tag keys for the same object must be unique. For object tag limitations, please refer to [Object tag limitations](https://docs.byteplus.com/docs/tos/docs-managing-file-labels#%E5%AF%B9%E8%B1%A1%E6%A0%87%E7%AD%BE%E9%99%90%E5%88%B6%E8%AF%B4%E6%98%8E).


<span id="7d882408"></span>
## Setting tags for an object

TOS enables the classification of objects within a bucket using tags. You can configure lifecycle rules for objects that share the same tags. The following code demonstrates how to set object tags.

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

            var tags = new []
            {
                new Tag
                {
                    Key = "key1",
                    Value = "value1"
                },
                new Tag
                {
                    Key = "key2",
                    Value = "value2"
                }
            };
            
            try
            {
                var putObjectTaggingInput = new PutObjectTaggingInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    TagSet = new TagSet{Tags = tags},
                    VersionID = "",
                };

                var putObjectTaggingOutput = client.PutObjectTagging(putObjectTaggingInput);
                Console.WriteLine("PutObjectTagging succeeded, Request ID {0}", putObjectTaggingOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("PutObjectTagging failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("PutObjectTagging failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("PutObjectTagging failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("PutObjectTagging failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("PutObjectTagging failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("PutObjectTagging failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id="e5398f23"></span>
## Getting tags of an object

After setting object tags, you can retrieve the object's tag information based on relevant criteria. When versioning is enabled for a bucket, TOS returns the tag information of the object's current version by default. You can obtain the tag information of a specific version by specifying the object's version.

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
                var getObjectTaggingInput = new GetObjectTaggingInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    VersionID = "",
                };

                var getObjectTaggingOutput = client.GetObjectTagging(getObjectTaggingInput);
                Console.WriteLine("GetObjectTagging succeeded, Request ID {0}", getObjectTaggingOutput.RequestID);
                foreach (var tag in getObjectTaggingOutput.TagSet.Tags)
                {
                    Console.WriteLine("Tag key: {0}, tag value: {1}", tag.Key, tag.Value);
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("GetObjectTagging failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("GetObjectTagging failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("GetObjectTagging failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("GetObjectTagging failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("GetObjectTagging failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("GetObjectTagging failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id="e5457aaf"></span>
## Deleting tags from an object

You may delete any unnecessary tag information as required. When versioning is enabled for a bucket, TOS deletes only the tag information of the object's current version by default. You can delete the tag information of a specific version by specifying the object's version ID.

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
                var deleteObjectTaggingInput = new DeleteObjectTaggingInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    VersionID = "",
                };

                var deleteObjectTaggingOutput = client.DeleteObjectTagging(deleteObjectTaggingInput);
                Console.WriteLine("DeleteObjectTagging succeeded, Request ID {0}", deleteObjectTaggingOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("DeleteObjectTagging failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("DeleteObjectTagging failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("DeleteObjectTagging failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("DeleteObjectTagging failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("DeleteObjectTagging failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("DeleteObjectTagging failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id="56fcf6b5"></span>
## Related documentation

For API documentation on object tagging, see [PutObjectTagging](https://docs.byteplus.com/docs/tos/reference-putobjecttagging-).
