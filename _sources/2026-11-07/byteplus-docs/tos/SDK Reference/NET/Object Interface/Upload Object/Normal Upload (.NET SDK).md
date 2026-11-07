---
title: "Normal Upload (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-upload-net-sdk"
---

Standard upload refers to uploading a single object via the PutObject method, which supports four forms: uploading a string (character stream), uploading bytes (byte stream), uploading a network stream, and uploading a local file.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Before uploading objects, you must ensure that your account has the tos:PutObject permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading an object, the object name must comply with the naming conventions. For more information, please refer to [Object Naming Conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage, with internal partitions that store object index data. To maximize the horizontal scalability of your upload and download throughput and reduce the likelihood of hot partitions, avoid using lexicographically incremental object naming. For more information, please [see Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. When multi\-versioning is enabled for a bucket, the original object is retained, and a new version number is generated to identify the newly uploaded object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5LiK5Lyg5a2X56ym5Liy"></span>
### Upload String

The following code uploads string data to the `example.txt` file in the `example_dir` directory of TOS via the PutObject interface.

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
            var objectContent = "Hello TOS";
            var objectKey = "example_dir/example.txt";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                byte[] binaryData = Encoding.UTF8.GetBytes(objectContent);
                using (MemoryStream requestContent = new MemoryStream(binaryData))
                {
                    var putObjectInput = new PutObjectInput()
                    {
                        Bucket = bucketName,
                        Key = objectKey,
                        Content = requestContent
                    };
                    var putObjectOutput = client.PutObject(putObjectInput);
                    Console.WriteLine("Put object succeeded, ETag: {0} ", putObjectOutput.ETag);
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


<span id=".5LiK5Lyg572R57uc5rWB"></span>
### Upload Network Stream

The following code uses the PutObject API to upload network stream data to the `example.txt` file under the `example_dir` directory in TOS.

```C#
using System;
using System.Net;
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
                var request = (HttpWebRequest)WebRequest.Create("https://www.byteplus.com/en/");
                request.Method = WebRequestMethods.Http.Get;
                var response = (HttpWebResponse)request.GetResponse();

                var putObjectInput = new PutObjectInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    Content = response.GetResponseStream()
                };

                var putObjectOutput = client.PutObject(putObjectInput);
                Console.WriteLine("Put object succeeded, request id: {0} ", putObjectOutput.RequestID);
                response.Close();
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


<span id=".5LiK5Lyg5pys5Zyw5paH5Lu25rWB"></span>
### Upload Local File Stream

The following code uploads the specified file stream to the `example_dir` directory in TOS as the `example.txt` file using the PutObject API.

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
            var localFileName = "/usr/local/test.txt";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                using (var fileStream = File.OpenRead(localFileName))
                {
                    var putObjectInput = new PutObjectInput()
                    {
                        Bucket = bucketName,
                        Key = objectKey,
                        Content = fileStream
                    };

                    var putObjectOutput = client.PutObject(putObjectInput);
                    Console.WriteLine("Put object succeeded, request id: {0} ", putObjectOutput.RequestID);
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


<span id=".5LiK5Lyg5pys5Zyw5paH5Lu2"></span>
### Upload Local File

The following code uses the PutObjectFromFile interface to specify a file path and upload the file to the specified `example_dir` directory in TOS as `example.txt`.

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
            var objectKey = "example_dir/example.txt";
            var localFileName = "/usr/local/test.txt";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var putObjectFromFileInput = new PutObjectFromFileInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    FilePath = localFileName
                };

                var putObjectFromFileOutput = client.PutObjectFromFile(putObjectFromFileInput);
                Console.WriteLine("Put object succeeded, request id: {0} ", putObjectFromFileOutput.RequestID);
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


<span id=".5LiK5Lyg5pe26K6-572u5a-56LGh5YWD5pWw5o2u5L-h5oGv"></span>
### Setting Object Metadata Information During Upload

The following code uploads string data to the `example_dir` directory's `example.txt` file using the PutObject API. During upload, the object storage type is set to Infrequent Access Storage, the access permission is configured as private, and file metadata is specified.

```C#
using System;
using System.Collections.Generic;
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

            var objectContent = "Hello TOS";
            var objectKey = "example_dir/example.txt";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var binaryData = Encoding.UTF8.GetBytes(objectContent);
                using (var requestContent = new MemoryStream(binaryData))
                {
                    var putObjectInput = new PutObjectInput
                    {
                        Bucket = bucketName,
                        Key = objectKey,
                        ACL = ACLType.ACLPrivate,
                        StorageClass = StorageClassType.StorageClassIa,
                        Meta = new Dictionary<string, string> { { "key", "value" } },
                        Content = requestContent
                    };
                    var putObjectOutput = client.PutObject(putObjectInput);
                    Console.WriteLine("Put object succeeded, ETag: {0} ", putObjectOutput.ETag);
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
