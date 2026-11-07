---
title: "Standard Download (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-download-net-sdk"
---

You can download objects from a specified bucket using the GetObject interface. Before using this interface, please ensure that you have read access to this object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Before downloading an object, you must ensure that your account has the tos:GetObject permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the tos:GetObjectVersion permission to download a specified version of an object. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object in large quantities simultaneously, your access speed will be limited by TOS bandwidth and regional restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. For more information on accessing TOS through CDN, see [Accelerating access to TOS resources using CDN](https://docs.byteplus.com/docs/6349/106079).


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5LiL6L295a-56LGh5Yiw5YaF5a2Y"></span>
### Download an object to memory

The following code is used to download objects into memory.

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
                var getObjectInput = new GetObjectInput
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    ResponseContentType = "application/json",
                    ResponseContentEncoding = "deflate"
                };
                var getObjectOutput = client.GetObject(getObjectInput);
                Console.WriteLine("GetObject succeeded, request id {0}", getObjectOutput.RequestID);
                Console.WriteLine("GetObject succeeded, content type {0}", getObjectOutput.ContentType);
                Console.WriteLine("GetObject succeeded, content encoding {0}", getObjectOutput.ContentEncoding);
                Console.WriteLine("GetObject succeeded, content length {0}", getObjectOutput.ContentLength);
                using (var reader = new StreamReader(getObjectOutput.Content))
                {
                    Console.WriteLine("GetObject succeeded, content {0}", reader.ReadToEnd());
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


<span id=".5LiL6L295a-56LGh5Yiw5pys5Zyw"></span>
### Download an object locally

The following code downloads an object from TOS to the specified local path.

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
            var downloadFilePath = "example_dir/example.txt";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var getObjectToFileInput = new GetObjectToFileInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    FilePath = downloadFilePath
                };
                var getObjectToFileOutput = client.GetObjectToFile(getObjectToFileInput);
                Console.WriteLine("GetObjectToFile succeeded, request id {0}", getObjectToFileOutput.RequestID);
                Console.WriteLine("GetObjectToFile succeeded, content length {0}", getObjectToFileOutput.ContentLength);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("GetObjectToFile failed, request id {0}", ex.RequestID);
                Console.WriteLine("GetObjectToFile failed, status code {0}", ex.StatusCode);
                Console.WriteLine("GetObjectToFile failed, response error code {0}", ex.Code);
                Console.WriteLine("GetObjectToFile failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("GetObjectToFile failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("GetObjectToFile failed, {0}", ex.Message);
            }
        }
    }
}
```
