---
title: "List Multi-Version Objects (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-multi-version-objects-net-sdk"
---

This API is used to list multiversion objects in a bucket. This API returns a maximum of 1,000 multiversion objects in the bucket for each request. You can use request parameters to define the selection criteria for the objects to list.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

Before listing multi\-version objects, you must ensure that your account has the tos:ListBucketVersions permission for the bucket. For detailed instructions, see [IAM Policy Overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters


|**Parameter** |**Description** |
|---|---|
|Prefix |The prefix of the current query result. |
|Delimiter |Character used to group object names. |
|MaxKeys |Returns the maximum number of objects to enumerate.<br><br>Value: greater than 0 and less than or equal to 1000<br><br>Default value: 1000 |
|EncodingType |Encode the returned content and specify the encoding type.<br><br>Default value: None |
|KeyMarker |List the starting positions of multi\-version objects. Objects are listed in alphabetical order after the specified start. This is typically the value of `next_marker` returned by the previous request. |
|VersionIdMarker |Used in conjunction with `KeyMarker`, this setting returns a list of multi\-version objects sorted in dictionary order starting after the specified value. Obtain `VersionIdMarker` from the previous listing results. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".566A5Y2V5YiX5Li-"></span>
### Brief Enumeration

The following code is used to list up to 10 multi\-version objects in the specified storage bucket.

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
                var listObjectVersionsInput = new ListObjectVersionsInput()
                {
                    Bucket = bucketName,
                    MaxKeys = 10
                };
                var listObjectVersionsOutput = client.ListObjectVersions(listObjectVersionsInput);
                foreach (var obj in listObjectVersionsOutput.Versions)
                {
                    Console.WriteLine("Object Key: {0}", obj.Key);
                    Console.WriteLine("Object VersionID: {0}", obj.VersionID);
                    Console.WriteLine("Object Last Modified: {0}", obj.LastModified);
                    Console.WriteLine("Object Is Latest Version: {0}", obj.IsLatest);
                }

                foreach (var deleteMarker in listObjectVersionsOutput.DeleteMarkers)
                {
                    Console.WriteLine("Delete Marker Key: {0}", deleteMarker.Key);
                    Console.WriteLine("Delete Marker VersionID: {0}", deleteMarker.VersionID);
                    Console.WriteLine("Delete Marker Last Modified: {0}", deleteMarker.LastModified);
                    Console.WriteLine("Delete Marker Is Latest Version: {0}", deleteMarker.IsLatest);
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("ListObjectVersions failed, request id {0}", ex.RequestID);
                Console.WriteLine("ListObjectVersions failed, status code {0}", ex.StatusCode);
                Console.WriteLine("ListObjectVersions failed, response error code {0}", ex.Code);
                Console.WriteLine("ListObjectVersions failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("ListObjectVersions failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("ListObjectVersions failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
### List all objects with the specified prefix

The following code enumerates all multi\-version objects with the specified prefix in the storage bucket, including objects with delete markers.

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
                var versionIdMarker = "";

                while (truncated)
                {
                    var listObjectVersionsInput = new ListObjectVersionsInput()
                    {
                        Bucket = bucketName,
                        MaxKeys = 10,
                        Prefix = prefix,
                        KeyMarker = marker,
                        VersionIDMarker = versionIdMarker
                    };
                    var listObjectVersionsOutput = client.ListObjectVersions(listObjectVersionsInput);
                    foreach (var obj in listObjectVersionsOutput.Versions)
                    {
                        Console.WriteLine("Object Key: {0}", obj.Key);
                        Console.WriteLine("Object VersionID: {0}", obj.VersionID);
                        Console.WriteLine("Object Last Modified: {0}", obj.LastModified);
                        Console.WriteLine("Object Is Latest Version: {0}", obj.IsLatest);
                    }

                    foreach (var deleteMarker in listObjectVersionsOutput.DeleteMarkers)
                    {
                        Console.WriteLine("Delete Marker Key: {0}", deleteMarker.Key);
                        Console.WriteLine("Delete Marker VersionID: {0}", deleteMarker.VersionID);
                        Console.WriteLine("Delete Marker Last Modified: {0}", deleteMarker.LastModified);
                        Console.WriteLine("Delete Marker Is Latest Version: {0}", deleteMarker.IsLatest);
                    }

                    truncated = listObjectVersionsOutput.IsTruncated;
                    marker = listObjectVersionsOutput.NextKeyMarker;
                    versionIdMarker = listObjectVersionsOutput.NextVersionIDMarker;
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("ListObjectVersions failed, request id {0}", ex.RequestID);
                Console.WriteLine("ListObjectVersions failed, status code {0}", ex.StatusCode);
                Console.WriteLine("ListObjectVersions failed, response error code {0}", ex.Code);
                Console.WriteLine("ListObjectVersions failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("ListObjectVersions failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("ListObjectVersions failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5YiX5Li-5omA5pyJ5a-56LGh"></span>
### Enumerate all objects

The following code enumerates all multi\-version objects in the specified bucket, including objects with delete markers.

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
                var versionIdMarker = "";

                while (truncated)
                {
                    var listObjectVersionsInput = new ListObjectVersionsInput()
                    {
                        Bucket = bucketName,
                        MaxKeys = 1000,
                        KeyMarker = marker,
                        VersionIDMarker = versionIdMarker
                    };
                    var listObjectVersionsOutput = client.ListObjectVersions(listObjectVersionsInput);
                    foreach (var obj in listObjectVersionsOutput.Versions)
                    {
                        Console.WriteLine("Object Key: {0}", obj.Key);
                        Console.WriteLine("Object VersionID: {0}", obj.VersionID);
                        Console.WriteLine("Object Last Modified: {0}", obj.LastModified);
                        Console.WriteLine("Object Is Latest Version: {0}", obj.IsLatest);
                    }

                    foreach (var deleteMarker in listObjectVersionsOutput.DeleteMarkers)
                    {
                        Console.WriteLine("Delete Marker Key: {0}", deleteMarker.Key);
                        Console.WriteLine("Delete Marker VersionID: {0}", deleteMarker.VersionID);
                        Console.WriteLine("Delete Marker Last Modified: {0}", deleteMarker.LastModified);
                        Console.WriteLine("Delete Marker Is Latest Version: {0}", deleteMarker.IsLatest);
                    }

                    truncated = listObjectVersionsOutput.IsTruncated;
                    marker = listObjectVersionsOutput.NextKeyMarker;
                    versionIdMarker = listObjectVersionsOutput.NextVersionIDMarker;
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("ListObjectVersions failed, request id {0}", ex.RequestID);
                Console.WriteLine("ListObjectVersions failed, status code {0}", ex.StatusCode);
                Console.WriteLine("ListObjectVersions failed, response error code {0}", ex.Code);
                Console.WriteLine("ListObjectVersions failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("ListObjectVersions failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("ListObjectVersions failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5YiX5Li-55uu5b2V5LiL55qE5a-56LGh5ZKM5a2Q55uu5b2V"></span>
### List objects and subdirectories within the directory

TOS supports only the concept of objects; by creating an object with a size of zero and a name ending with a slash (/), it is possible to simulate directory functionality.

The `Delimiter` and `Prefix` parameters can be used to simulate the functionality of a directory. The explanation is as follows:


* Set `Delimiter` to`/`At the same time, set `Prefix` to empty, and the objects and subdirectory information in the root directory will be returned.

* Set `Delimiter` to`/`At the same time, set `Prefix` to the subdirectory `subfiledir`; the objects and subdirectories within the subdirectory will be returned.


The following code is used to enumerate multi\-version objects and subdirectories within a directory. During enumeration, all versions of objects are returned, while only the latest version of each subdirectory is listed.

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
                var versionIdMarker = "";
                var delimiter = "/";

                while (truncated)
                {
                    var listObjectVersionsInput = new ListObjectVersionsInput()
                    {
                        Bucket = bucketName,
                        MaxKeys = 1000,
                        KeyMarker = marker,
                        VersionIDMarker = versionIdMarker,
                        Delimiter = delimiter
                    };
                    var listObjectVersionsOutput = client.ListObjectVersions(listObjectVersionsInput);

                    foreach (var prefix in listObjectVersionsOutput.CommonPrefixes)
                    {
                        Console.WriteLine("Sub Dir: {0}", prefix.Prefix);
                    }

                    foreach (var obj in listObjectVersionsOutput.Versions)
                    {
                        Console.WriteLine("Object Key: {0}", obj.Key);
                        Console.WriteLine("Object VersionID: {0}", obj.VersionID);
                        Console.WriteLine("Object Last Modified: {0}", obj.LastModified);
                        Console.WriteLine("Object Is Latest Version: {0}", obj.IsLatest);
                    }

                    foreach (var deleteMarker in listObjectVersionsOutput.DeleteMarkers)
                    {
                        Console.WriteLine("Delete Marker Key: {0}", deleteMarker.Key);
                        Console.WriteLine("Delete Marker VersionID: {0}", deleteMarker.VersionID);
                        Console.WriteLine("Delete Marker Last Modified: {0}", deleteMarker.LastModified);
                        Console.WriteLine("Delete Marker Is Latest Version: {0}", deleteMarker.IsLatest);
                    }

                    truncated = listObjectVersionsOutput.IsTruncated;
                    marker = listObjectVersionsOutput.NextKeyMarker;
                    versionIdMarker = listObjectVersionsOutput.NextVersionIDMarker;
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("ListObjectVersions failed, request id {0}", ex.RequestID);
                Console.WriteLine("ListObjectVersions failed, status code {0}", ex.StatusCode);
                Console.WriteLine("ListObjectVersions failed, response error code {0}", ex.Code);
                Console.WriteLine("ListObjectVersions failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("ListObjectVersions failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("ListObjectVersions failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to the API for listing multi\-version objects, see [ListObjectsVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions).
