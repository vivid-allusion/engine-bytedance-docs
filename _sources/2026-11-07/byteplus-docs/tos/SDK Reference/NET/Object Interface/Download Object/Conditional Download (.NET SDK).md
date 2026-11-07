---
title: "Conditional Download (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Limited-download-net-sdk"
---

The TOS .NET SDK supports configuring constraints for object downloads. When downloading an object, you can specify constraints such as the object's ETag or modification time. The server will return the object data only if the object's information meets the specified conditions; otherwise, an appropriate error will be returned. This article describes how to download objects under restrictive conditions.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Before downloading an object, you must ensure that your account has the `tos:GetObject` permission. For specific instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* For buckets with versioning enabled, you must have the `tos:GetObjectVersion` permission to download a specified version of an object. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If an application downloads the same object in large quantities at the same time, your access speed will be limited by TOS bandwidth and geographic restrictions. We recommend that you use CDN to enhance the performance while reducing your costs. For more information on accessing TOS through CDN, see [Accelerating Access to TOS Resources Using CDN](https://docs.byteplus.com/docs/6349/106079).


<span id=".6ZmQ5Yi25p2h5Lu26K-05piO"></span>
## Explanation of Constraints

The following are the restrictions supported by TOS.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Different conditions can be combined; for example, both If\-Modified\-Since and If\-Unmodified\-Since may be present simultaneously, and both If\-Match and If\-None\-Match may also coexist.</div>


* <div data-tips="true" data-tips-type="tip">You can also use the HeadObject interface of the TOS .NET SDK to obtain the Etag information of an object.</div>




|Parameter |Description |
|---|---|
|If\-Match |The object is returned only if the incoming `ETag` matches the object's `ETag`; otherwise, a `412 Precondition Failed` is returned. |
|If\-None\-Match |The object is returned only if the incoming `ETag` does not match the object's `ETag`; otherwise, `304 Not Modified` is returned. |
|If\-Modified\-Since |The object is returned only if it has been modified since the specified time; otherwise, 304 Not Modified is returned. |
|If\-Unmodified\-Since |The object is returned only if it has not been modified since the specified time; otherwise, `412 Precondition Failed` is returned. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to restrict object downloads based on the If\-Modified\-Since and IfUnmodifiedSince conditions.

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
            var date = new DateTime(2022, 10, 24, 0, 0, 0, DateTimeKind.Utc);

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var getObjectInput = new GetObjectInput
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    IfModifiedSince = date
                };
                var getObjectOutput = client.GetObject(getObjectInput);
                using (var reader = new StreamReader(getObjectOutput.Content))
                {
                    Console.WriteLine("GetObject succeeded, content {0}", reader.ReadToEnd());
                    getObjectOutput.Content.Close();
                }
            }
            catch (TosServerException ex)
            {
                if (ex.StatusCode == 304)
                {
                    Console.WriteLine("Object not modify, request id {0}", ex.RequestID);
                }
                else
                {
                    Console.WriteLine("GetObject failed, request id {0}", ex.RequestID);
                    Console.WriteLine("GetObject failed, status code {0}", ex.StatusCode);
                    Console.WriteLine("GetObject failed, response error code {0}", ex.Code);
                    Console.WriteLine("GetObject failed, response error message {0}", ex.Message);
                }
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("GetObject failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("GetObject failed, {0}", ex.Message);
            }

            try
            {
                var getObjectInput = new GetObjectInput
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    IfUnmodifiedSince = date
                };
                var getObjectOutput = client.GetObject(getObjectInput);
                using (var reader = new StreamReader(getObjectOutput.Content))
                {
                    Console.WriteLine("GetObject succeeded, content {0}", reader.ReadToEnd());
                    getObjectOutput.Content.Close();
                }
            }
            catch (TosServerException ex)
            {
                if (ex.StatusCode == 412)
                {
                    Console.WriteLine("Object modify, request id {0}", ex.RequestID);
                }
                else
                {
                    Console.WriteLine("GetObject failed, request id {0}", ex.RequestID);
                    Console.WriteLine("GetObject failed, status code {0}", ex.StatusCode);
                    Console.WriteLine("GetObject failed, response error code {0}", ex.Code);
                    Console.WriteLine("GetObject failed, response error message {0}", ex.Message);
                }
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

For a detailed introduction to the conditional download API, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
