---
title: "Manage Object Metadata (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-metadata-net-sdk"
---

Object metadata refers to the attribute descriptions of an object, encompassing both HTTP standard attributes (HTTP Header) and user\-defined metadata (User Meta).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Only the object owner has permission to set object metadata.

* When setting user\-defined metadata, the user\-defined metadata key in English letters supports only lowercase letters and does not allow spaces or other special characters.


<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters

The TOS .NET SDK enables users to add and modify metadata for objects that have already been uploaded. TOS supports the use of the following six request headers to modify object metadata. When downloading an object or performing a HEAD request, these values are set in the HTTP header fields and returned to the client. The request headers are as follows:


|  |Description |
|---|---|
|Content\-Type |Object content type, |
|Cache\-Control |Specifies the caching behavior when the object is downloaded. |
|Expires |Specifies the cache expiration time as defined in RFC 2616. |
|Content\-Disposition |Specifies the default filename of the object when downloaded. |
|Content\-Encoding |Specifies the content encoding of the object when downloaded. |
|Content\-Language |Specifies the content language of the object when downloaded. |
|x\-tos\-meta\-\* |Metadata information set when setting the Meta field using the SDK. When this object is queried, metadata will be included in the Header of the returned message. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5pmu6YCa5LiK5Lyg5pe26K6-572u5YWD5pWw5o2u5L-h5oGv"></span>
### Specifying metadata information during standard upload

The following code is used to set metadata, including cache policy and cache expiration time, during file upload.

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
                byte[] binaryData = Encoding.UTF8.GetBytes(objectContent);
                using (MemoryStream requestContent = new MemoryStream(binaryData))
                {
                    var putObjectInput = new PutObjectInput()
                    {
                        Bucket = bucketName,
                        Key = objectKey,
                        Meta = new Dictionary<string, string>() { { "key", "value" } },
                        ContentType = "text/html",
                        ContentLanguage = "zh-cn",
                        CacheControl = "no-store",
                        Expires = DateTime.Now.AddHours(1),
                        ContentDisposition = "example.png",
                        ContentEncoding = "deflate",
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


<span id=".5YiG54mH5LiK5Lyg5pe26K6-572u5YWD5pWw5o2u5L-h5oGv"></span>
### Configuring metadata during multipart upload

The following code is used to set metadata information, such as cache policy and cache expiration time, during multipart upload.

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
                var createMultipartUploadInput = new CreateMultipartUploadInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    Meta = new Dictionary<string, string>() { { "key", "value" } },
                    ContentType = "text/html",
                    ContentLanguage = "zh-cn",
                    CacheControl = "no-store",
                    Expires = DateTime.Now.AddHours(1),
                    ContentDisposition = "example.png",
                    ContentEncoding = "deflate",
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

            Int64 partSize = 20 * 1024 * 1024;
            var fi = new FileInfo(localFileName);
            var fileSize = fi.Length;
            var partCount = fileSize / partSize;
            if (fileSize % partSize != 0)
            {
                partCount++;
            }

            var parts = new UploadedPart[partCount];

            try
            {
                using (var fileStream = File.Open(localFileName, FileMode.Open, FileAccess.Read))
                {
                    for (var i = 0; i < partCount; i++)
                    {
                        var offset = partSize * i;
                        fileStream.Seek(offset, 0);
                        var contentSize = (partSize < fileSize - offset) ? partSize : (fileSize - offset);
                        var UploadPartInput = new UploadPartInput()
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
                var completeMultipartUploadInput = new CompleteMultipartUploadInput()
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


<span id=".6YCa6L-HLXNldG9iamVjdG1ldGEt6K6-572u5a-56LGh5YWD5pWw5o2u5L-h5oGv"></span>
### Set object metadata information using SetObjectMeta.

The following code is used to update object metadata, such as caching policy and cache expiration time, via the SetObjectMeta interface.

```C#
using System;
using System.Collections.Generic;
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
                var setObjectMetaInput = new SetObjectMetaInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    Meta = new Dictionary<string, string>() { { "key", "value" } },
                    ContentType = "text/html",
                    ContentLanguage = "zh-cn",
                    CacheControl = "no-store",
                    Expires = DateTime.Now.AddHours(1),
                    ContentDisposition = "example.png",
                    ContentEncoding = "deflate",
                };

                var setObjectMetaOutput = client.SetObjectMeta(setObjectMetaInput);
                Console.WriteLine("Set object meta succeeded, request id: {0} ", setObjectMetaOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("Set object meta failed, request id {0}", ex.RequestID);
                Console.WriteLine("Set object meta failed, status code {0}", ex.StatusCode);
                Console.WriteLine("Set object meta failed, response error code {0}", ex.Code);
                Console.WriteLine("Set object meta failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("Set object meta failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("Set object meta failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5p-l6K-i5a-56LGh5YWD5pWw5o2u5L-h5oGv77yI5Yik5pat5a-56LGh5piv5ZCm5a2Y5Zyo77yJ"></span>
### Query Object Metadata Information (Determine Whether the Object Exists)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before retrieving object metadata, you must ensure that your account has the tos:GetObject permission. For specific steps, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-overview_6">IAM Policy Overview</a>.</div>


The following code is used to query object metadata and determine whether the object exists. If the object does not exist, an error message will be returned.

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
                var headObjectInput = new HeadObjectInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                };

                var headObjectOutput = client.HeadObject(headObjectInput);
                Console.WriteLine("HeadObject succeeded, Request ID: {0} ", headObjectOutput.RequestID);
                Console.WriteLine("HeadObject succeeded, Response ContentLanguage: {0} ",
                    headObjectOutput.ContentLanguage);
                Console.WriteLine("HeadObject succeeded, Response ContentDisposition: {0} ",
                    headObjectOutput.ContentDisposition);
                Console.WriteLine("HeadObject succeeded, Response ContentEncoding: {0} ",
                    headObjectOutput.ContentEncoding);
                Console.WriteLine("HeadObject succeeded, Response CacheControl: {0} ", headObjectOutput.CacheControl);
                Console.WriteLine("HeadObject succeeded, Response ContentType: {0} ", headObjectOutput.ContentType);
                Console.WriteLine("HeadObject succeeded, Response Expires: {0} ", headObjectOutput.Expires);
            }
            catch (TosServerException ex)
            {
                if (ex.StatusCode == 404)
                {
                    Console.WriteLine("Object not found");
                }
                else
                {
                    Console.WriteLine("HeadObject failed, Request ID {0}", ex.RequestID);
                    Console.WriteLine("HeadObject failed, Status Code {0}", ex.StatusCode);
                    Console.WriteLine("HeadObject failed, Response Error Code {0}", ex.Code);
                    Console.WriteLine("HeadObject failed, Response Error Message {0}", ex.Message);
                }
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("HeadObject failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("HeadObject failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to the API interface for setting object metadata, see [SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta).
