---
title: "Scoped Download (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Scope-download-net-sdk"
---

If you only need to retrieve a portion of the data within an object, you can use range downloading to obtain data from a specified range. This article introduces range downloading.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Before performing a range download, you must ensure that your account has the tos:GetObject permission. For detailed instructions, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the tos:GetObjectVersion permission to download a specified version of an object. For detailed instructions, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object in large quantities at the same time, your access speed will be limited by TOS bandwidth and regional restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. For more information on accessing TOS through CDN, see [Accelerating Access to TOS Resources Using CDN](https://docs.byteplus.com/docs/6349/106079).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to download bytes 32 to 64 of an object in a bucket.

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
            var objectKey = "example_dir/example.txt";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var getObjectInput = new GetObjectInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    RangeStart = 32,
                    RangeEnd = 64
                };
                var getObjectOutput = client.GetObject(getObjectInput);
                Console.WriteLine("GetObject succeeded, request id {0}", getObjectOutput.RequestID);
                Console.WriteLine("GetObject succeeded, content type {0}", getObjectOutput.ContentType);
                Console.WriteLine("GetObject succeeded, content encoding {0}", getObjectOutput.ContentEncoding);
                Console.WriteLine("GetObject succeeded, content length {0}", getObjectOutput.ContentLength);
                using (var reader = new StreamReader(getObjectOutput.Content))
                {
                    Console.WriteLine("GetObject failed, content {0}", reader.ReadToEnd());
                    getObjectOutput.Content.Close();
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("GetObject failed, request id {0}", ex.RequestID);
                Console.WriteLine("GetObject failed, status code {0}", ex.StatusCode);
                Console.WriteLine("GetObject failed, response error code {0}", ex.Code);
                Console.WriteLine("GetObject failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("GetObject failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("GetObject failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to the range download API, please refer to [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
