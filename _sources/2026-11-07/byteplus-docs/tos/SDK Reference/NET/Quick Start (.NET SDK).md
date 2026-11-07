---
title: "Quick Start (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start-net-sdk"
---

This document describes how to quickly perform common operations using the TOS .NET SDK, including creating buckets, uploading objects, downloading objects, listing objects, and deleting objects.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [The SDK has been installed](https://docs.byteplus.com/docs/tos/Instal-the-net-sdk).

2. [The client has been initialized](https://docs.byteplus.com/docs/tos/Initializing-the-client-side-net-sdk).


<span id=".5Yib5bu65qG2"></span>
## Creating a Bucket

A bucket is the globally unique namespace in TOS, functioning as a container for data and used to store object data. The following code demonstrates how to use the CreateBucket method to create a new storage bucket:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about creating buckets, see <a href="https://docs.byteplus.com/docs/tos/Create-a-bucket-net-sdk">Creating Buckets</a>.</div>


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
            var endpoint = "*** Provide your endpoint ***";
            var region = "*** Provide your region ***";
            var bucketName = "*** Provide your bucket name ***";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var createBucketInput = new CreateBucketInput()
                {
                    Bucket = bucketName
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


<span id=".5LiK5Lyg5a-56LGh"></span>
## Uploads an object.

After the bucket is successfully created, objects can be uploaded to the bucket. The following code demonstrates how to upload a string to an already created bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about uploading objects, see <a href="https://docs.byteplus.com/docs/tos/Normal-upload-net-sdk">Uploading Objects</a>.</div>


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
            var objectKey = "*** Provide your object key ***";
            var objectContent = "object content";
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


<span id=".5LiL6L295a-56LGh"></span>
## Download Object

The following code demonstrates how to download an existing object from a bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about download objects, see <a href="https://docs.byteplus.com/docs/tos/Normal-download-net-sdk">Download Objects</a>.</div>


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
            var objectKey = "*** Provide your object key ***";
            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var getObjectInput = new GetObjectInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                };
                var putObjectOutput = client.GetObject(getObjectInput);
                Console.WriteLine("Get object succeeded, requestId: {0} ", putObjectOutput.RequestID);
                Console.WriteLine("Get object succeeded, ETag: {0} ", putObjectOutput.ETag);
                Console.WriteLine("Get object succeeded, status code: {0} ", putObjectOutput.StatusCode);
                using (var reader = new StreamReader(putObjectOutput.Content))
                {
                    var body = reader.ReadToEnd();
                    Console.WriteLine("Get object succeeded, body: {0} ", body);
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("Get object failed, request id {0}", ex.RequestID);
                Console.WriteLine("Get object failed, status code {0}", ex.StatusCode);
                Console.WriteLine("Get object failed, response error code {0}", ex.Code);
                Console.WriteLine("Get object failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Get object failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Get object failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5YiX5Li-5a-56LGh"></span>
## Enumeration of Objects

The following code demonstrates how to list the objects already in the bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about enumerating objects, see <a href="https://docs.byteplus.com/docs/tos/Normal-download-net-sdk">Enumerating Objects</a>.</div>


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
                var listObjectsInput = new ListObjectsInput()
                {
                    Bucket = bucketName,
                };
    
                var listObjectsOutput = client.ListObjects(listObjectsInput);
                Console.WriteLine("List object Request id, {0}", listObjectsOutput.RequestID);
    
                if (!listObjectsOutput.IsTruncated) {
                    listObjectsInput.Marker = listObjectsOutput.NextMarker;
                    listObjectsOutput = client.ListObjects(listObjectsInput);
                    Console.WriteLine("List object Request id, {0}", listObjectsOutput.RequestID);
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("List object failed, request Id {0}", ex.RequestID);
                Console.WriteLine("List object failed, status code {0}", ex.StatusCode);
                Console.WriteLine("List object failed, response error code {0}", ex.Code);
                Console.WriteLine("List object failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("List object failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("List object failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5Yig6Zmk5a-56LGh"></span>
## When you delete an object

The following code demonstrates how to delete an existing object from a bucket.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about deleting objects, see <a href="https://docs.byteplus.com/docs/tos/Delete-objects-net-sdk">Deleting Objects</a>.</div>


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
            var objectKey = "*** Provide your object key ***";
            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var deleteObjectInput = new DeleteObjectInput()
                {
                    Bucket = bucketName,
                    Key = objectKey
                };
    
                var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                Console.WriteLine("Delete object Request id, {0}", deleteObjectOutput.RequestID);
                Console.WriteLine("Delete object response status code, {0}", deleteObjectOutput.StatusCode);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("Delete object failed, request id {0}", ex.RequestID);
                Console.WriteLine("Delete object failed, status code {0}", ex.StatusCode);
                Console.WriteLine("Delete object failed, response error code {0}", ex.Code);
                Console.WriteLine("Delete object failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Delete object failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Delete object failed, {0}", ex.Message);
            }
        }
    }
}
```
