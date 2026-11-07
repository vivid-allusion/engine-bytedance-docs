---
title: "Chunked Copy (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-copy-net-sdk"
---

When an object exceeds 5 GiB in size, you can use the UploadPartCopy API to perform a multipart copy operation.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Copying objects between storage buckets in different regions is not supported.

* When copying an object, the account must have read permission for the source object and write permission for the destination bucket.

* When copying an object, you can either retain all metadata (default) or specify new metadata. However, the ACL was not retained; instead, it was set to private.


<span id=".5YiG54mH5ou36LSd5q2l6aqk"></span>
## Sharded Copy Procedures

Shard copying comprises the following three steps:


1. Initialize the multipart copy task using create_multipart_upload.

2. Perform multipart copy using upload_part_copy.

3. Merge file parts using complete_multipart_upload.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to perform multipart copying of specified objects from the source bucket to the target bucket within the same region, with each part size set to 20 MB.

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
            var srcBucketName = "*** Provide your bucket name ***";
            var dstBucketName = "*** Provide your dst bucket name ***";
            var srcObjectKey = "srcObjectKey";
            var dstObjectKey = "objectKey";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var headObjectInput = new HeadObjectInput()
                {
                    Bucket = srcBucketName,
                    Key = srcObjectKey,
                };
                var headObjectOutput = client.HeadObject(headObjectInput);
                var totalSize = headObjectOutput.ContentLength;

                Int64 partSize = 20 * 1024 * 1024;
                var partCount = totalSize / partSize;
                if (totalSize % partSize != 0)
                {
                    partCount++;
                }

                var parts = new UploadedPart[partCount];

                var createMultipartUploadInput = new CreateMultipartUploadInput()
                {
                    Bucket = dstBucketName,
                    Key = dstObjectKey
                };
                var createMultipartUploadOutput = client.CreateMultipartUpload(createMultipartUploadInput);
                var uploadId = createMultipartUploadOutput.UploadID;

                for (var i = 0; i < partCount; i++)
                {
                    var offset = partSize * i;
                    var contentSize = (partSize < totalSize - offset) ? partSize : (totalSize - offset);

                    var uploadPartCopyInput = new UploadPartCopyInput()
                    {
                        Bucket = dstBucketName,
                        Key = dstObjectKey,
                        SrcBucket = srcBucketName,
                        SrcKey = srcObjectKey,
                        UploadID = uploadId,
                        PartNumber = i + 1,
                        CopySourceRangeStart = offset,
                        CopySourceRangeEnd = offset + contentSize - 1
                    };
                    var uploadPartCopyOutput = client.UploadPartCopy(uploadPartCopyInput);
                    parts[i] = new UploadedPart { PartNumber = i + 1, ETag = uploadPartCopyOutput.ETag };
                    Console.WriteLine("UploadPartCopy succeeded, request id {0}", uploadPartCopyOutput.RequestID);
                }

                var completeMultipartUploadInput = new CompleteMultipartUploadInput()
                {
                    Bucket = dstBucketName,
                    Key = dstObjectKey,
                    UploadID = uploadId,
                    Parts = parts
                };
                var completeMultipartUploadOutput = client.CompleteMultipartUpload(completeMultipartUploadInput);
                Console.WriteLine("CompleteMultipartUpload succeeded, request id {0}",
                    completeMultipartUploadOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("Copy failed, request id {0}", ex.RequestID);
                Console.WriteLine("Copy failed, status code {0}", ex.StatusCode);
                Console.WriteLine("Copy failed, response error code {0}", ex.Code);
                Console.WriteLine("Copy failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Copy failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Copy failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* For a detailed introduction to the API interface for creating multipart upload tasks, please refer to [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For a detailed introduction to the multipart copy API, see [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy).

* For a detailed description of the API interface for merging parts, see [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).
