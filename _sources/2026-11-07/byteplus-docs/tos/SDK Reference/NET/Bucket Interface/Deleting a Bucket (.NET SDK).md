---
title: "Deleting a Bucket (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-bucket-net-sdk"
---

When you no longer need to retain a bucket (Bucket), you may delete it to avoid incurring additional charges.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before deleting a bucket, ensure that all data within the bucket has been removed.


* If versioning is enabled for the current bucket, please ensure that all current and historical version objects within the bucket have been deleted. For detailed instructions, see [Delete Object](https://docs.byteplus.com/docs/tos/docs-versioning-related-operations#%E5%BD%BB%E5%BA%95%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6).

* If there are unmerged shards in the bucket, please ensure that all shard data is deleted. For detailed instructions, please see [Deleting Shards](https://docs.byteplus.com/docs/tos/docs-managing-parts#%E5%88%A0%E9%99%A4%E5%88%86%E7%89%87).

* If your bucket contains a large number of objects, you can configure batch deletion of objects by setting lifecycle rules. For instructions, see [Configuring lifecycle rules](https://docs.byteplus.com/docs/6349/75028).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Once a bucket is deleted, it cannot be restored. Please proceed with caution.

* Before deleting a bucket, you must ensure that your account has the tos:DeleteBucket permission. For detailed procedures, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to delete a bucket.

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

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var deleteBucketInput = new DeleteBucketInput()
                {
                    Bucket = bucketName,
                };
                var deleteBucketOutput = client.DeleteBucket(deleteBucketInput);
                Console.WriteLine("Delete bucket succeeded, request id {0} ", deleteBucketOutput.RequestID);
                Console.WriteLine("Delete bucket succeeded, status code {0} ", deleteBucketOutput.StatusCode);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("Delete bucket failed, request id {0}", ex.RequestID);
                Console.WriteLine("Delete bucket failed, status code {0}", ex.StatusCode);
                Console.WriteLine("Delete bucket failed, response error code {0}", ex.Code);
                Console.WriteLine("Delete bucket failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Delete bucket failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Delete bucket failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to the API for deleting buckets, see [DeleteBucket](https://docs.byteplus.com/docs/tos/reference-deletebucket).
