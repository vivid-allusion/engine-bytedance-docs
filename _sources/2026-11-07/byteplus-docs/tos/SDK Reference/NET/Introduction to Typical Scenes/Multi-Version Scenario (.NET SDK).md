---
title: "Multi-Version Scenario (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Multi-version-scenes-net-sdk"
---

Version control is applied to all objects within the bucket. By enabling bucket versioning, you can restore an object to any previous version after accidental deletion or overwriting. Currently, multi\-version support is available for interfaces including GetObject, GetObjectACL, CopyObject, UploadPartCopy, DeleteObject, etc. When invoking the relevant interfaces, you can specify the exact version of the target object by using the optional parameter VersionID.

<span id=".5LiL6L295aSa54mI5pys5a-56LGh"></span>
## Download Objects with Multiple Versions

The following versions are used to download the specified version object.

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
            var versionID = "your object version id";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var getObjectInput = new GetObjectInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    VersionID = versionID
                };
                var getObjectOutput = client.GetObject(getObjectInput);
                Console.WriteLine("GetObject succeeded, request id {0}", getObjectOutput.RequestID);
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


<span id=".5Yig6Zmk5aSa54mI5pys5a-56LGh"></span>
## Deleting Multi\-Version Objects

The following code is used to delete objects of a specified version.

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
            var versionID = "*** Provide object Version ID";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var deleteObjectInput = new DeleteObjectInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    VersionID = versionID
                };

                var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                Console.WriteLine("DeleteObject succeeded, Request ID {0}", deleteObjectOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("DeleteObject failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("DeleteObject failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("DeleteObject failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("DeleteObject failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("DeleteObject failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("DeleteObject failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5riF56m65byA5ZCv5aSa54mI5pys55qE5qG2"></span>
## Emptying a versioned bucket

The following code is used to clear an entire versioned storage bucket, including deleting all object versions (including delete markers) and all incomplete multipart uploads.

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
                var keyMarker = "";
                var isTruncated = true;

                while (isTruncated)
                {
                    var listObjectVersionsInput = new ListObjectVersionsInput()
                    {
                        Bucket = bucketName,
                        MaxKeys = 1000,
                        KeyMarker = keyMarker,
                    };
                    var listObjectVersionsOutput = client.ListObjectVersions(listObjectVersionsInput);

                    foreach (var obj in listObjectVersionsOutput.Versions)
                    {
                        var deleteObjectInput = new DeleteObjectInput()
                        {
                            Bucket = bucketName,
                            Key = obj.Key,
                            VersionID = obj.VersionID
                        };
                        var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                        Console.WriteLine("Delete {0}, Request ID {1}", obj.Key, deleteObjectOutput.RequestID);
                    }

                    foreach (var deleteMarker in listObjectVersionsOutput.DeleteMarkers)
                    {
                        var deleteObjectInput = new DeleteObjectInput()
                        {
                            Bucket = bucketName,
                            Key = deleteMarker.Key,
                            VersionID = deleteMarker.VersionID
                        };
                        var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                        Console.WriteLine("Delete {0}, Request ID {1}", deleteMarker.Key, deleteObjectOutput.RequestID);
                    }

                    isTruncated = listObjectVersionsOutput.IsTruncated;
                    keyMarker = listObjectVersionsOutput.NextKeyMarker;
                }

                keyMarker = "";
                isTruncated = true;
                while (isTruncated)
                {
                    var listMultipartUploadsInput = new ListMultipartUploadsInput()
                    {
                        Bucket = bucketName,
                        MaxUploads = 1000,
                        KeyMarker = keyMarker
                    };
                    var listMultipartUploadsOutput = client.ListMultipartUploads(listMultipartUploadsInput);

                    foreach (var upload in listMultipartUploadsOutput.Uploads)
                    {
                        var abortMultipartUploadInput = new AbortMultipartUploadInput()
                        {
                            Bucket = bucketName,
                            Key = upload.Key,
                            UploadID = upload.UploadID,
                        };
                        var abortMultipartUploadOutput = client.AbortMultipartUpload(abortMultipartUploadInput);
                        Console.WriteLine("AbortMultipartUpload UploadID {0}, Request ID {1}", upload.UploadID,
                            abortMultipartUploadOutput.RequestID);

                        isTruncated = listMultipartUploadsOutput.IsTruncated;
                        keyMarker = listMultipartUploadsOutput.NextKeyMarker;
                    }
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("Clear Bucket failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("Clear Bucket failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("Clear Bucket failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("Clear Bucket failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Clear Bucket failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Clear Bucket failed, {0}", ex.Message);
            }
        }
    }
}
```
