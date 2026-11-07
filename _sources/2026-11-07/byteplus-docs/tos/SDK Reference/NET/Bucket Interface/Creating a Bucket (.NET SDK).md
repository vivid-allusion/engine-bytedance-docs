---
title: "Creating a Bucket (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-a-bucket-net-sdk"
---

A Bucket in TOS is a globally unique namespace that serves as a container for storing Object data. The name of a newly created bucket must be unique within TOS. This document describes how to create a bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* The [naming conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts) for storage buckets are as follows:

   * Can only contain lowercase letters (a\-z), numbers, and hyphens (\-).

   * Must start and end with a number or letter.

   * Length must be between 3 and 63 characters.

* When accessing TOS via other BytePlus products within the same region, it is recommended to use the internal network Endpoint. For more information about regions and Endpoints, see [Regions and Access Domain Names](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before creating a storage bucket, you must ensure that your account has the tos:CreateBucket permission. You can grant the appropriate permissions through IAM policies. For detailed steps, please refer to [IAM Policies](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5oyH5a6aLWFjbA=="></span>
### Specify ACL

The following code is used to specify the ACL when creating a storage bucket.

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
                var createBucketInput = new CreateBucketInput()
                {
                    Bucket = bucketName,
                    ACL = ACLType.ACLPrivate
                };
                var createBucketOutput = client.CreateBucket(createBucketInput);
                Console.WriteLine("Create bucket succeeded, request id {0} ", createBucketOutput.RequestID);
                Console.WriteLine("Create bucket succeeded, status code {0} ", createBucketOutput.StatusCode);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("Create bucket failed, request id {0}", ex.RequestID);
                Console.WriteLine("Create bucket failed, status code {0}", ex.StatusCode);
                Console.WriteLine("Create bucket failed, response error code {0}", ex.Code);
                Console.WriteLine("Create bucket failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Create bucket failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Create bucket failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5oyH5a6a5a2Y5YKo57G75Z6L"></span>
### Specify Storage Type

The following code is used to specify the storage type when creating a bucket.

```C#
using System;
using TOS;
using TOS.Error;
using TOS.Model;

var ak = Environment.GetEnvironmentVariable("TOS_ACCESS_KEY");
var sk = Environment.GetEnvironmentVariable("TOS_SECRET_KEY");
var endpoint = "your endpoint";
var region = "your region";
var bucketName = "*** Provide your bucket name ***";

var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

try
{
    var createBucketInput = new CreateBucketInput()
    {
        Bucket = bucketName,
        StorageClass = StorageClassType.StorageClassIa
    };
    var createBucketOutput = client.CreateBucket(createBucketInput);
    Console.WriteLine("Create bucket succeeded, request id {0} ", createBucketOutput.RequestID);
    Console.WriteLine("Create bucket succeeded, status code {0} ", createBucketOutput.StatusCode);
}
catch (TosServerException ex)
{
    Console.WriteLine("Create bucket failed, request id {0}", ex.RequestID);
    Console.WriteLine("Create bucket failed, status code {0}", ex.StatusCode);
    Console.WriteLine("Create bucket failed, response error code {0}", ex.Code);
    Console.WriteLine("Create bucket failed, response error message {0}", ex.Message);
}
catch (TosClientException ex)
{
    Console.WriteLine("Create bucket failed, error message {0}", ex.Message);
}
catch (Exception ex)
{
    Console.WriteLine("Create bucket failed, {0}", ex.Message);
}
```


<span id=".5oyH5a6aLWF6Leexu-Weiw=="></span>
### Specify Availability Zone Type

The following code demonstrates how to specify the Availability Zone type when creating a bucket.

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
                var createBucketInput = new CreateBucketInput()
                {
                    Bucket = bucketName,
                    AzRedundancy = AzRedundancyType.AzRedundancyMultiAz
                };
                var createBucketOutput = client.CreateBucket(createBucketInput);
                Console.WriteLine("Create bucket succeeded, request id {0} ", createBucketOutput.RequestID);
                Console.WriteLine("Create bucket succeeded, status code {0} ", createBucketOutput.StatusCode);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("Create bucket failed, request id {0}", ex.RequestID);
                Console.WriteLine("Create bucket failed, status code {0}", ex.StatusCode);
                Console.WriteLine("Create bucket failed, response error code {0}", ex.Code);
                Console.WriteLine("Create bucket failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Create bucket failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Create bucket failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For an introduction to the API interface for bucket creation, see [CreateBucket](https://docs.byteplus.com/docs/tos/Create-a-bucket-net-sdk).
