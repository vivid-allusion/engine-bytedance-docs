---
title: "List Buckets (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-buckets-net-sdk"
---

A bucket (Bucket) in TOS serves as a globally unique namespace, functioning as a data container for storing object (Object) data. This article describes how to use the TOS .NET SDK `listBuckets` interface to enumerate all storage buckets under the current account across all regions that meet specified criteria.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Before listing buckets, you must ensure that your account has the tos:ListBuckets permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* This interface returns all buckets in every region associated with the current account.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code enumerates all buckets across all regions for the current account.

```C#
using System;
using TOS;
using TOS.Error;

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

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var listBucketsOutput = client.ListBuckets();
                Console.WriteLine("List bucket succeeded, request id {0} ", listBucketsOutput.RequestID);
                Console.WriteLine("List bucket succeeded, status code {0} ", listBucketsOutput.StatusCode);
                foreach (var bucket in listBucketsOutput.Buckets)
                {
                    Console.WriteLine("Bucket Name: {0}", bucket.Name);
                    Console.WriteLine("Bucket CreationDate: {0}", bucket.CreationDate);
                    Console.WriteLine("Bucket Location: {0}", bucket.Location);
                    Console.WriteLine("Bucket ExtranetEndpoint: {0}", bucket.ExtranetEndpoint);
                    Console.WriteLine("Bucket IntranetEndpoint: {0}", bucket.IntranetEndpoint);
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("List bucket failed, request id {0}", ex.RequestID);
                Console.WriteLine("List bucket failed, status code {0}", ex.StatusCode);
                Console.WriteLine("List bucket failed, response error code {0}", ex.Code);
                Console.WriteLine("List bucket failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("List bucket failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("List bucket failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to the API interface for listing buckets, see [ListBuckets](https://docs.byteplus.com/docs/tos/reference-listbuckets).
