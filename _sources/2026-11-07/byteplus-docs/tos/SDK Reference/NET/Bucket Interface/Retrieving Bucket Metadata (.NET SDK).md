---
title: "Retrieving Bucket Metadata (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-metadata-net-sdk"
---

You can obtain information about a bucket using HeadBucket, and determine whether the bucket exists based on the HTTP response code. This article describes how to obtain bucket metadata and determine whether a bucket exists.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Before retrieving bucket metadata, you must ensure that your account already has the tos:HeadBucket permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If the bucket does not exist, this interface will return a 404 error. This interface is also commonly used to determine whether the bucket exists.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5Yik5pat5qG25piv5ZCm5a2Y5Zyo"></span>
### Determine whether the bucket exists

The following code is used to check whether the bucket exists.

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
                var headBucketInput = new HeadBucketInput()
                {
                    Bucket = bucketName,
                };
                var headBucketOutput = client.HeadBucket(headBucketInput);
                Console.WriteLine("Head bucket succeeded, request id {0} ", headBucketOutput.RequestID);
                Console.WriteLine("Head bucket succeeded, status code {0} ", headBucketOutput.StatusCode);
            }
            catch (TosServerException ex)
            {
                if (ex.StatusCode == 404)
                {
                    Console.WriteLine("Bucket not found");
                }
                Console.WriteLine("Head bucket failed, request id {0}", ex.RequestID);
                Console.WriteLine("Head bucket failed, status code {0}", ex.StatusCode);
                Console.WriteLine("Head bucket failed, response error code {0}", ex.Code);
                Console.WriteLine("Head bucket failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Head bucket failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Head bucket failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".6I635Y-W5qG25YWD5pWw5o2u5L-h5oGv"></span>
### Retrieve Bucket Metadata Information

The following code is used to retrieve bucket metadata information.

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
                var headBucketInput = new HeadBucketInput()
                {
                    Bucket = bucketName,
                };
                var headBucketOutput = client.HeadBucket(headBucketInput);
                Console.WriteLine("Head bucket succeeded, request id {0} ", headBucketOutput.RequestID);
                Console.WriteLine("Head bucket succeeded, status code {0} ", headBucketOutput.StatusCode);
                Console.WriteLine("Bucket Region {0}", headBucketOutput.Region);
                Console.WriteLine("Bucket Storage Class {0}", headBucketOutput.StorageClass);
                Console.WriteLine("Bucket Az Redundancy {0}", headBucketOutput.AzRedundancy);
            }
            catch (TosServerException ex)
            {
                if (ex.StatusCode == 404)
                {
                    Console.WriteLine("Bucket not found");
                }
                Console.WriteLine("Head bucket failed, request id {0}", ex.RequestID);
                Console.WriteLine("Head bucket failed, status code {0}", ex.StatusCode);
                Console.WriteLine("Head bucket failed, response error code {0}", ex.Code);
                Console.WriteLine("Head bucket failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Head bucket failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Head bucket failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to the API interface for obtaining bucket metadata, see [HeadBucket](https://docs.byteplus.com/docs/tos/reference-headbucket).
