---
title: "Object Enumeration (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-net-sdk"
---

This document describes how to use ListObject to enumerate all objects within a specified bucket, files with a designated prefix, files and subdirectories within a specified directory.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters


|**Parameter** |**Description** |
|---|---|
|Prefix |The prefix of the current query results. |
|Delimiter |Character used to group object names. |
|Marker |Specifies where to start listing. Objects are listed in alphabetical order after the specified start. This is typically the value of `next_marker` returned by the previous request. |
|MaxKeys |Returns the maximum number of objects to enumerate.<br><br>Value: greater than 0 and less than or equal to 1000<br><br>Default value: 1000 |
|EncodingType |Encode the returned content and specify the encoding type.<br><br>Default value: None |


#{.custom\-md\-table}#

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### Brief Enumeration

The following code enumerates 10 objects in the specified bucket.

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
                    MaxKeys = 10
                };

                var listObjectsOutput = client.ListObjects(listObjectsInput);
                foreach (var obj in listObjectsOutput.Contents)
                {
                    Console.WriteLine("Object Key: {0}", obj.Key);
                    Console.WriteLine("Object LastModified: {0}", obj.LastModified);
                    Console.WriteLine("Object ETag: {0}", obj.ETag);
                    Console.WriteLine("Object Size: {0}", obj.Size);
                    Console.WriteLine("Object Owner: {0}", obj.Owner);
                    Console.WriteLine("Object StorageClass: {0}", obj.StorageClass);
                    Console.WriteLine("Object HashCrc64ecma: {0}", obj.HashCrc64ecma);
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


<span id=".5YiG6aG15YiX5Li-"></span>
### Paginated Listing

The following code is used to paginate the listing of objects in a specified storage bucket, including retrieving the first 1,000 objects and then paginating to obtain the next 1,000 objects.

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
                    MaxKeys = 1000
                };

                var listObjectsOutput = client.ListObjects(listObjectsInput);
                foreach (var obj in listObjectsOutput.Contents)
                {
                    Console.WriteLine("Object Key: {0}", obj.Key);
                    Console.WriteLine("Object LastModified: {0}", obj.LastModified);
                    Console.WriteLine("Object ETag: {0}", obj.ETag);
                    Console.WriteLine("Object Size: {0}", obj.Size);
                    Console.WriteLine("Object Owner: {0}", obj.Owner);
                    Console.WriteLine("Object StorageClass: {0}", obj.StorageClass);
                    Console.WriteLine("Object HashCrc64ecma: {0}", obj.HashCrc64ecma);
                }

                listObjectsInput = new ListObjectsInput()
                {
                    Bucket = bucketName,
                    MaxKeys = 1000,
                    Marker = listObjectsOutput.NextMarker
                };
                listObjectsOutput = client.ListObjects(listObjectsInput);

                foreach (var obj in listObjectsOutput.Contents)
                {
                    Console.WriteLine("Object Key: {0}", obj.Key);
                    Console.WriteLine("Object LastModified: {0}", obj.LastModified);
                    Console.WriteLine("Object ETag: {0}", obj.ETag);
                    Console.WriteLine("Object Size: {0}", obj.Size);
                    Console.WriteLine("Object Owner: {0}", obj.Owner);
                    Console.WriteLine("Object StorageClass: {0}", obj.StorageClass);
                    Console.WriteLine("Object HashCrc64ecma: {0}", obj.HashCrc64ecma);
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


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### Enumerate all objects with the specified prefix

The following code is used to enumerate all objects in the storage bucket with the specified prefix.

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
            var prefix = "*** Provide your object key prefix ***";

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
                        Prefix = prefix,
                        MaxKeys = 1000,
                        Marker = marker
                    };

                    var listObjectsOutput = client.ListObjects(listObjectsInput);
                    foreach (var obj in listObjectsOutput.Contents)
                    {
                        Console.WriteLine("Object Key: {0}", obj.Key);
                        Console.WriteLine("Object LastModified: {0}", obj.LastModified);
                        Console.WriteLine("Object ETag: {0}", obj.ETag);
                        Console.WriteLine("Object Size: {0}", obj.Size);
                        Console.WriteLine("Object Owner: {0}", obj.Owner);
                        Console.WriteLine("Object StorageClass: {0}", obj.StorageClass);
                        Console.WriteLine("Object HashCrc64ecma: {0}", obj.HashCrc64ecma);
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


<span id=".5YiG6aG15YiX5Li-5qG25YaF5omA5pyJ5a-56LGh"></span>
### List all objects in the bucket with pagination

The following code is used to list all objects in the specified storage bucket with pagination.

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
                        Marker = marker
                    };

                    var listObjectsOutput = client.ListObjects(listObjectsInput);
                    foreach (var obj in listObjectsOutput.Contents)
                    {
                        Console.WriteLine("Object Key: {0}", obj.Key);
                        Console.WriteLine("Object LastModified: {0}", obj.LastModified);
                        Console.WriteLine("Object ETag: {0}", obj.ETag);
                        Console.WriteLine("Object Size: {0}", obj.Size);
                        Console.WriteLine("Object Owner: {0}", obj.Owner);
                        Console.WriteLine("Object StorageClass: {0}", obj.StorageClass);
                        Console.WriteLine("Object HashCrc64ecma: {0}", obj.HashCrc64ecma);
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


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
### List the files and subdirectories in the specified directory.

TOS recognizes only the concept of objects. Directory functionality can be simulated by creating an object with a size of zero and a name ending with a slash (/).

The functionality of a directory can be simulated using the `Delimiter` and `Prefix` parameters, as explained below:


* Set `Delimiter` to`/`At the same time, if `Prefix` is set to empty, the objects and subdirectory information in the root directory will be returned.

* Set `Delimiter` to`/`At the same time, set `Prefix` to the subdirectory `subfiledir`; the objects and subdirectories within the subdirectory will be returned.


The following code enumerates the objects and subdirectories within the directory.

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
