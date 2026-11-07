---
title: "Incremental Upload (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-net-sdk"
---

Append upload refers to using the AppendObject interface to append new data to the end of existing object data. The object type created through append upload is an appendable type (Appendable Object), which allows data to be appended to the end of the object. Objects created through standard upload and multipart upload are of the Normal Object type and do not support appending data.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Before performing an append upload operation, you must ensure that your account has the tos:PutObject permission. For detailed instructions, please refer to the [Permissions Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading an object, the object name must comply with the naming conventions. For more information, see [Object Naming Conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage. Its internal partitions store object index data. To maximize the throughput of object uploads and downloads during horizontal scaling, and to reduce the likelihood of hotspot partitions, please avoid using lexicographically incremental object naming. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. When multi\-versioning is enabled for a bucket, the original object is retained, and a new version number is generated to identify the newly uploaded object.

* Append upload does not support chunk\-encoded requests. When performing append upload for network streams, please retrieve data iteratively and then append upload.


<span id=".6ZmQ5Yi26K-05piO"></span>
## Limitation Statement

AppendObject has the following restrictions:


* The size of the object after appending must not exceed 5 GiB.

* Performing a PutObject operation on an object created through AppendObject will result in the object being overwritten, and the object type changing from "Appendable" to "Normal". Conversely, objects uploaded through PutObject cannot be appended with additional data.

* Objects created through AppendObject cannot be copied.

* If an object is in Infrequent Access Storage or Flashback Archive, data cannot be appended using AppendObject.

* If your bucket has versioning enabled or suspended, you cannot use the AppendObject API.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to first append and upload a specified character stream to a designated file, and then append and upload a local file from a specified path to the same file.

```C#
using System;
using System.IO;
using System.Text;
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
            var objectContent = "your append object value";
            var objectKey = "example_dir/example.txt";
            var localFileName = "/usr/local/test.txt";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var binaryData = Encoding.UTF8.GetBytes(objectContent);
                AppendObjectOutput appendObjectOutput;

                using (var requestContent = new MemoryStream(binaryData))
                {
                    var appendObjectInput = new AppendObjectInput
                    {
                        Bucket = bucketName,
                        Key = objectKey,
                        Content = requestContent
                    };

                    appendObjectOutput = client.AppendObject(appendObjectInput);
                    Console.WriteLine("Append object succeeded, request id: {0} ", appendObjectOutput.RequestID);
                }

                using (var fileStream = File.OpenRead(localFileName))
                {
                    var appendObjectInput = new AppendObjectInput
                    {
                        Bucket = bucketName,
                        Key = objectKey,
                        Offset = appendObjectOutput.NextAppendOffset,
                        Content = fileStream
                    };

                    appendObjectOutput = client.AppendObject(appendObjectInput);
                    Console.WriteLine("Append object succeeded, request id: {0} ", appendObjectOutput.RequestID);
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("Put object failed, request id {0}", ex.RequestID);
                Console.WriteLine("Put object failed, status code {0}", ex.StatusCode);
                Console.WriteLine("Put object failed, response error code {0}", ex.Code);
                Console.WriteLine("Put object failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Put object failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Put object failed, {0}", ex.Message);
            }
        }
    }
}
```
