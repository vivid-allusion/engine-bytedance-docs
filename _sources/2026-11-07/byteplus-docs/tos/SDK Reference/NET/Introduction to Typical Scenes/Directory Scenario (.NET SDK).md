---
title: "Directory Scenario (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Directory-scenes-net-sdk"
---

TOS is based solely on the concept of objects and stores data using a flat structure. To facilitate object grouping and simplify permission management, you can organize objects using a directory hierarchy.

<span id=".5Yib5bu655uu5b2V"></span>
## Create Directory

The following code is used to create a directory.

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

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                using (MemoryStream requestContent = new MemoryStream(Encoding.UTF8.GetBytes("")))
                {
                    var putObjectInput = new PutObjectInput()
                    {
                        Bucket = bucketName,
                        Key = "exampledir/",
                        Content = requestContent
                    };
                    var putObjectOutput = client.PutObject(putObjectInput);
                    Console.WriteLine("Put object succeeded, ETag: {0} ", putObjectOutput.ETag);
                }

                using (MemoryStream requestContent = new MemoryStream(Encoding.UTF8.GetBytes("")))
                {
                    var putObjectInput = new PutObjectInput()
                    {
                        Bucket = bucketName,
                        Key = "exampledir/test/",
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


<span id=".5qih5ouf55uu5b2V5p-l6K-i"></span>
## Simulated Directory Query

TOS supports only the concept of objects. Directory functionality can be simulated by creating an object with a size of zero whose name ends with a slash (/).

The directory functionality can be simulated using the `Delimiter` and `Prefix` parameters, as explained below:


* Set `Delimiter` to`/`At the same time, set `Prefix` to empty; the objects and subdirectory information under the root directory will be returned.

* Set `Delimiter` to`/`At the same time, set `Prefix` to the subdirectory `subfiledir`; the objects and subdirectories of the subdirectory will be returned.


The following code enumerates the objects and subdirectories in the root directory.

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
                var truncated = true;
                var marker = "";

                while (truncated)
                {
                    var listObjectsInput = new ListObjectsInput()
                    {
                        Bucket = bucketName,
                        MaxKeys = 1000,
                        Delimiter = "/",
                        Marker = marker
                    };

                    var listObjectsOutput = client.ListObjects(listObjectsInput);
                    foreach (var obj in listObjectsOutput.CommonPrefixes)
                    {
                        Console.WriteLine("Sub Dir: {0}", obj.Prefix);
                    }

                    foreach (var obj in listObjectsOutput.Contents)
                    {
                        Console.WriteLine("Obj: {0}", obj.Key);
                    }

                    truncated = listObjectsOutput.IsTruncated;
                    marker = listObjectsOutput.NextMarker;
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("ListObjects failed, request id {0}", ex.RequestID);
                Console.WriteLine("ListObjects failed, status code {0}", ex.StatusCode);
                Console.WriteLine("ListObjects failed, response error code {0}", ex.Code);
                Console.WriteLine("ListObjects failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("ListObjects failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("ListObjects failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5Yig6Zmk55uu5b2V5LiL55qE5paH5Lu2"></span>
## Delete files in the directory

The following code is used to delete all files under the `exampledir/` directory in the storage bucket.

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
                var truncated = true;
                var marker = "";

                while (truncated)
                {
                    var listObjectsInput = new ListObjectsInput()
                    {
                        Bucket = bucketName,
                        MaxKeys = 1000,
                        Prefix = "exampledir/",
                        Marker = marker
                    };

                    var listObjectsOutput = client.ListObjects(listObjectsInput);

                    foreach (var obj in listObjectsOutput.Contents)
                    {
                        var deleteObjectInput = new DeleteObjectInput()
                        {
                            Bucket = bucketName,
                            Key = obj.Key
                        };
                        var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                        Console.WriteLine("DeleteObject Request ID: {0}", deleteObjectOutput.RequestID);
                    }

                    truncated = listObjectsOutput.IsTruncated;
                    marker = listObjectsOutput.NextMarker;
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("DeleteObject failed, request id {0}", ex.RequestID);
                Console.WriteLine("DeleteObject failed, status code {0}", ex.StatusCode);
                Console.WriteLine("DeleteObject failed, response error code {0}", ex.Code);
                Console.WriteLine("DeleteObject failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("DeleteObject failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("DeleteObject failed, {0}", ex.Message);
            }
        }
    }
}
```
