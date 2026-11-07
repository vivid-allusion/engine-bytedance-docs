---
title: "Standard Copy (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-copy-net-sdk"
---

You can use the copy_object interface to copy objects between buckets within the same region, or to copy objects within the same bucket. During copying, you can specify new metadata or retain the metadata of the source object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Copying objects between storage buckets across regions is not supported.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to copy objects between storage buckets within the same region.

```C#
using System;
using System.IO;
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
            var dstBucketName = "*** Provide your dst bucket name ***";
            var srcObjectKey = "srcObjectKey";
            var dstObjectKey = "objectKey";

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

                copyObjectInput = new CopyObjectInput()
                {
                    Bucket = bucketName,
                    Key = dstObjectKey,
                    SrcBucket = bucketName,
                    SrcKey = srcObjectKey,
                    ACL = ACLType.ACLPrivate,
                    StorageClass = StorageClassType.StorageClassIa,
                };
                copyObjectOutput = client.CopyObject(copyObjectInput);
                Console.WriteLine("CopyObject succeeded, request id {0}", copyObjectOutput.RequestID);
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


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to the API interface for ordinary copy operations, please refer to [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).
