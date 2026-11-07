---
title: "Upload Callback (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-callback-net-sdk"
---

An upload callback refers to the process in which the client includes a callback parameter in its request. Upon completion of the upload, the server sends a synchronous POST callback request to the third\-party application server specified in the callback. Only after the third\-party application server confirms receipt and returns a result are all results returned to the client.

For a detailed introduction to upload callback, please refer to [Upload Callback](https://docs.byteplus.com/docs/tos/Upload-callback).

<span id="9b4cf5b9"></span>
## Sample Code

<span id="d5de9160"></span>
### Implementation of upload callback for standard upload

```C#
using System;
using System.IO;
using System.Text;
using TOS;
using TOS.Error;
using TOS.Model;

namespace TestTos
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
            var callback = "your callback param";
            var callbackVar = "your callback custom variable";
            
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
                        Content = requestContent,
                        Callback = Convert.ToBase64String(Encoding.UTF8.GetBytes(callback)),
                        CallbackVar = Convert.ToBase64String(Encoding.UTF8.GetBytes(callbackVar))
                    };
                    var putObjectOutput = client.PutObject(putObjectInput);
                    Console.WriteLine("Put object succeeded, ETag: {0} ", putObjectOutput.ETag);
                    Console.WriteLine("Put object succeeded, CallbackResult: {0} ", putObjectOutput.CallbackResult);
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


<span id="04b3c44f"></span>
### Implementation of Callback Mechanism for Multipart Uploads

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
            var objectKey = "example_dir/example.txt";
            var localFileName = "/usr/local/test.txt";
            var callback = "your callback param";
            var callbackVar = "your callback custom variable";

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
                    Parts = parts,
                    Callback = Convert.ToBase64String(Encoding.UTF8.GetBytes(callback)),
                    CallbackVar = Convert.ToBase64String(Encoding.UTF8.GetBytes(callbackVar))
                };
                var completeMultipartUploadOutput = client.CompleteMultipartUpload(completeMultipartUploadInput);
                Console.WriteLine("CompleteMultipartUpload succeeded, request id {0}", completeMultipartUploadOutput.RequestID);
                Console.WriteLine("CompleteMultipartUpload succeeded, callback result {0}", completeMultipartUploadOutput.CallbackResult);
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
