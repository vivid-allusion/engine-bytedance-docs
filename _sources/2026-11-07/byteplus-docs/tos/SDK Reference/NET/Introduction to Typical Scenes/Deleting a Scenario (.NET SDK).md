---
title: "Deleting a Scenario (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-scenes-net-sdk"
---

This article presents example code for common object deletion scenarios.

<span id=".5Yig6Zmk55uu5b2V"></span>
## Delete Directory

The following code is used to delete objects under the specified directory `exampledir/`.

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


<span id=".5riF56m65qG2"></span>
## Empty Bucket

The following code is used to clear the entire bucket, including deleting all objects and all unmerged objects.

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
                var marker = "";
                var isTruncated = true;

                while (isTruncated)
                {
                    var listObjectInput = new ListObjectsInput()
                    {
                        Bucket = bucketName,
                        MaxKeys = 1000,
                        Marker = marker
                    };
                    var listObjectOutput = client.ListObjects(listObjectInput);

                    foreach (var obj in listObjectOutput.Contents)
                    {
                        var deleteObjectInput = new DeleteObjectInput()
                        {
                            Bucket = bucketName,
                            Key = obj.Key,
                        };
                        var deleteObjectOutput = client.DeleteObject(deleteObjectInput);
                        Console.WriteLine("Delete {0}, Request ID {1}", obj.Key, deleteObjectOutput.RequestID);
                    }

                    isTruncated = listObjectOutput.IsTruncated;
                    marker = listObjectOutput.NextMarker;
                }

                marker = "";
                isTruncated = true;
                while (isTruncated)
                {
                    var listMultipartUploadsInput = new ListMultipartUploadsInput()
                    {
                        Bucket = bucketName,
                        MaxUploads = 1000,
                        KeyMarker = marker
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
                        marker = listMultipartUploadsOutput.NextKeyMarker;
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


<span id=".5riF56m65byA5ZCv5aSa54mI5pys55qE5qG2"></span>
## Emptying a versioning\-enabled bucket

The following code is used to clear an entire storage bucket with versioning enabled, including the deletion of objects with multiple versions (including delete markers) and all unmerged objects.

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
