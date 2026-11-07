---
title: "Multipart Upload (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-upload-net-sdk"
---

If you need to upload large objects, it is recommended to divide them into multiple data blocks (parts) and upload each separately. Finally, invoke the merge parts operation to combine the uploaded data blocks into a single object.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Before initiating multipart upload, you must ensure that your account has the tos:PutObject permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To cancel a multipart upload task, you must have the tos:AbortMultipartUpload permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading an object, the object name must comply with the naming conventions. For more information, please refer to [Object Naming Conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for massive data storage. Its internal partitions store object index data. To horizontally scale the maximum throughput for uploading and downloading objects, and to reduce the probability of partitions becoming hotspots, please avoid using lexicographically incremental object naming. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. When bucket versioning is enabled, the original object is retained, and a new version number is generated to identify the newly uploaded object.


<span id=".5YiG54mH5LiK5Lyg5q2l6aqk"></span>
## Multipart Upload Procedure

Multipart upload using the TOS .NET SDK consists of the following three steps.


1. Initialize Multipart Upload Task

   Invoking the `createMultipartUpload` interface returns a globally unique `uploadId` created by TOS.

2. Upload Chunk

   Call the `uploadPart` interface to upload data chunks.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the same multipart upload task (identified by <code>uploadId</code>), the part number (<code>partNumber</code>) indicates the relative position of the part within the entire object. If data is uploaded multiple times using the same shard number, TOS will overwrite the existing data, and only the data from the most recent upload will be retained.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>uploadPart</code> API returns the MD5 value of the part data, which can be obtained through the <code>ETag</code> field. When merging parts, you must specify the information for all uploaded parts in the current multipart upload task, including the part number and ETag value.   </div>
   

3. Complete Multipart Upload

   After all parts have been uploaded, call the `completeMultipartUpload` API to merge all parts into a complete object.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5YiG54mH5LiK5Lyg5a6M5pW06L-H56iL"></span>
### Complete Process of Multipart Upload

The following code demonstrates the complete process of uploading a local file using multipart upload, while specifying the ACL as Private, setting the storage type to Infrequent Access Storage, and adding custom metadata during the upload.

```C#
using System;
using System.Collections.Generic;
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

            var uploadID = "";
            try
            {
                var createMultipartUploadInput = new CreateMultipartUploadInput
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    ACL = ACLType.ACLPrivate,
                    StorageClass = StorageClassType.StorageClassIa,
                    Meta = new Dictionary<string, string> { { "key", "value" } }
                };
                var createMultipartUploadOutput = client.CreateMultipartUpload(createMultipartUploadInput);
                uploadID = createMultipartUploadOutput.UploadID;
                Console.WriteLine("CreateMultipartUpload succeeded, request id {0}",
                    createMultipartUploadOutput.RequestID);
                Console.WriteLine("CreateMultipartUpload succeeded, upload id {0}", uploadID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("CreateMultipartUpload failed, request id {0}", ex.RequestID);
                Console.WriteLine("CreateMultipartUpload failed, status code {0}", ex.StatusCode);
                Console.WriteLine("CreateMultipartUpload failed, response error code {0}", ex.Code);
                Console.WriteLine("CreateMultipartUpload failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("CreateMultipartUpload failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("CreateMultipartUpload failed, {0}", ex.Message);
            }

            long partSize = 20 * 1024 * 1024;
            var fi = new FileInfo(localFileName);
            var fileSize = fi.Length;
            var partCount = fileSize / partSize;
            if (fileSize % partSize != 0) partCount++;
            var parts = new UploadedPart[partCount];

            try
            {
                using (var fileStream = File.Open(localFileName, FileMode.Open, FileAccess.Read))
                {
                    for (var i = 0; i < partCount; i++)
                    {
                        var offset = partSize * i;
                        fileStream.Seek(offset, 0);
                        var contentSize = partSize < fileSize - offset ? partSize : fileSize - offset;
                        var UploadPartInput = new UploadPartInput
                        {
                            Bucket = bucketName,
                            Key = objectKey,
                            UploadID = uploadID,
                            PartNumber = i + 1,
                            Content = fileStream,
                            ContentLength = contentSize
                        };
                        var uploadPartOutput = client.UploadPart(UploadPartInput);
                        parts[i] = new UploadedPart { PartNumber = i + 1, ETag = uploadPartOutput.ETag };
                        Console.WriteLine("UploadPart succeeded, request id {0}", uploadPartOutput.RequestID);
                    }
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("UploadPart failed, request id {0}", ex.RequestID);
                Console.WriteLine("UploadPart failed, status code {0}", ex.StatusCode);
                Console.WriteLine("UploadPart failed, response error code {0}", ex.Code);
                Console.WriteLine("UploadPart failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("UploadPart failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("UploadPart failed, {0}", ex.Message);
            }

            try
            {
                var completeMultipartUploadInput = new CompleteMultipartUploadInput
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    UploadID = uploadID,
                    Parts = parts
                };
                var completeMultipartUploadOutput = client.CompleteMultipartUpload(completeMultipartUploadInput);
                Console.WriteLine("CompleteMultipartUpload succeeded, request id {0}",
                    completeMultipartUploadOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("CompleteMultipartUpload failed, request id {0}", ex.RequestID);
                Console.WriteLine("CompleteMultipartUpload failed, status code {0}", ex.StatusCode);
                Console.WriteLine("CompleteMultipartUpload failed, response error code {0}", ex.Code);
                Console.WriteLine("CompleteMultipartUpload failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("CompleteMultipartUpload failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("CompleteMultipartUpload failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5YiX5Li-5bey5LiK5Lyg5YiG54mH"></span>
### List Uploaded Parts

The following code is used to list the information about uploaded parts of a specified object within a storage bucket.

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
            var uploadID = "*** Provide upload ID ***";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var truncated = true;
                var marker = 0;
                while (truncated)
                {
                    var createMultipartUploadInput = new ListPartsInput
                    {
                        Bucket = bucketName,
                        Key = objectKey,
                        UploadID = uploadID,
                        PartNumberMarker = marker
                    };
                    var listPartsOutput = client.ListParts(createMultipartUploadInput);
                    truncated = listPartsOutput.IsTruncated;
                    marker = listPartsOutput.NextPartNumberMarker;
                    Console.WriteLine("ListParts succeeded, request id {0}", listPartsOutput.RequestID);
                    Console.WriteLine("ListParts succeeded, upload id {0}", uploadID);
                    foreach (var part in listPartsOutput.Parts)
                    {
                        Console.WriteLine("ListParts succeeded, part number {0}", part.PartNumber);
                        Console.WriteLine("ListParts succeeded, part Etag {0}", part.ETag);
                        Console.WriteLine("ListParts succeeded, part size {0}", part.Size);
                    }
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("ListParts failed, request id {0}", ex.RequestID);
                Console.WriteLine("ListParts failed, status code {0}", ex.StatusCode);
                Console.WriteLine("ListParts failed, response error code {0}", ex.Code);
                Console.WriteLine("ListParts failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("ListParts failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("ListParts failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5Y-W5raI5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### Cancel Multipart Upload Task

You can cancel a multipart upload task using the AbortMultipartUpload API. After a multipart upload task is canceled, TOS will delete the already uploaded part data. You will no longer be able to perform any operations on this multipart upload task.

The following code is used to cancel a multipart upload task.

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
            var uploadID = "*** Provide upload ID ***";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var abortMultipartUploadInput = new AbortMultipartUploadInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    UploadID = uploadID,
                };
                var abortMultipartUploadOutput = client.AbortMultipartUpload(abortMultipartUploadInput);
                Console.WriteLine("AbortMultipartUpload succeeded, request id {0}", abortMultipartUploadOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("AbortMultipartUpload failed, request id {0}", ex.RequestID);
                Console.WriteLine("AbortMultipartUpload failed, status code {0}", ex.StatusCode);
                Console.WriteLine("AbortMultipartUpload failed, response error code {0}", ex.Code);
                Console.WriteLine("AbortMultipartUpload failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("AbortMultipartUpload failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("AbortMultipartUpload failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* For a detailed introduction to the API interface for creating multipart upload tasks, see [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For a detailed introduction to the UploadPart API, please refer to [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart).

* For a detailed introduction to the API for merging parts, see [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).

* For a detailed introduction to the API interface for aborting multipart upload tasks, please refer to [AbortMultipartUpload](https://docs.byteplus.com/docs/tos/reference-abortmultipartupload).
