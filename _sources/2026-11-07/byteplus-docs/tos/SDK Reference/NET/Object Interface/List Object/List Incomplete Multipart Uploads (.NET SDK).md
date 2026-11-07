---
title: "List Incomplete Multipart Uploads (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-unmerged-objects-net-sdk"
---

This interface is used to list incomplete multipart uploads in a bucket, returning up to 1,000 results.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the <code>IsTruncated</code> field in the response message is set to <code>true</code>, it indicates that there are still multipart uploads that have not been listed.</div>


* <div data-tips="true" data-tips-type="tip">The KeyMarker and <code>UploadIDMarker</code> request parameters can be used to list additional multipart uploads.</div>



<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

Before listing multipart uploads, you must ensure that your account has the tos:ListBucketMultipartUploads permission for the bucket. For detailed instructions, see [IAM policy overview](https://docs.byteplus.com/docs/tos/docs-overview_6).

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters


|**Parameter** |**Description** |
|---|---|
|Prefix |Specify the prefix name for objects to be returned in the listing. |
|Delimiter |Character used to group object names. |
|MaxUploads |Returns the maximum number of multipart uploads.<br><br>Value: Greater than 0 and less than or equal to 1,000<br><br>Default value: 1,000 |
|EncodingType |Encode the returned content and specify the encoding type.<br><br>Default value: None |
|KeyMarker |List the starting positions of multipart uploads. Objects are listed in alphabetical order after the specified start. This is typically the value of `nextMarker` returned by the previous request. |
|VersionIdMarker |Used in conjunction with `keyMarker`, this parameter specifies that the list of multipart uploads will be returned in lexicographical order after the value provided. Obtain `nextVersionIdMarker` from the previous listing results. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".566A5Y2V5YiX5Li-"></span>
### List a specified number of incomplete multipart uploads

The following code is used to list up to 10 incomplete multipart uploads in the specified bucket.

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
                var listMultipartUploadsInput = new ListMultipartUploadsInput()
                {
                    Bucket = bucketName,
                    MaxUploads = 10
                };
                var listMultipartUploadsOutput = client.ListMultipartUploads(listMultipartUploadsInput);
                foreach (var upload in listMultipartUploadsOutput.Uploads)
                {
                    Console.WriteLine("Object Key: {0}", upload.Key);
                    Console.WriteLine("Object UploadID: {0}", upload.UploadID);
                    Console.WriteLine("Object Owner: {0}", upload.Owner);
                    Console.WriteLine("Object StorageClass: {0}", upload.StorageClass);
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("ListMultipartUploads failed, request id {0}", ex.RequestID);
                Console.WriteLine("ListMultipartUploads failed, status code {0}", ex.StatusCode);
                Console.WriteLine("ListMultipartUploads failed, response error code {0}", ex.Code);
                Console.WriteLine("ListMultipartUploads failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("ListMultipartUploads failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("ListMultipartUploads failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5pyq5ZCI5bm255qE5YiG54mH5Lu75Yqh"></span>
### List all incomplete multipart uploads with the specified prefix

The following code is used to list all incomplete multipart uploads under the specified prefix in the specified bucket.

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
                    var listMultipartUploadsInput = new ListMultipartUploadsInput()
                    {
                        Bucket = bucketName,
                        MaxUploads = 1000,
                        KeyMarker = marker,
                        Prefix = prefix
                    };
                    var listMultipartUploadsOutput = client.ListMultipartUploads(listMultipartUploadsInput);
                    foreach (var upload in listMultipartUploadsOutput.Uploads)
                    {
                        Console.WriteLine("Object Key: {0}", upload.Key);
                        Console.WriteLine("Object UploadID: {0}", upload.UploadID);
                        Console.WriteLine("Object Owner: {0}", upload.Owner);
                        Console.WriteLine("Object StorageClass: {0}", upload.StorageClass);
                    }

                    truncated = listMultipartUploadsOutput.IsTruncated;
                    marker = listMultipartUploadsOutput.NextKeyMarker;
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("ListMultipartUploads failed, request id {0}", ex.RequestID);
                Console.WriteLine("ListMultipartUploads failed, status code {0}", ex.StatusCode);
                Console.WriteLine("ListMultipartUploads failed, response error code {0}", ex.Code);
                Console.WriteLine("ListMultipartUploads failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("ListMultipartUploads failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("ListMultipartUploads failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5YiX5Li-5omA5pyJ5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
### List all multipart uploads

The following code lists all incomplete multipart uploads in the specified bucket.

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
                    var listMultipartUploadsInput = new ListMultipartUploadsInput()
                    {
                        Bucket = bucketName,
                        MaxUploads = 1000,
                        KeyMarker = marker,
                    };
                    var listMultipartUploadsOutput = client.ListMultipartUploads(listMultipartUploadsInput);
                    foreach (var upload in listMultipartUploadsOutput.Uploads)
                    {
                        Console.WriteLine("Object Key: {0}", upload.Key);
                        Console.WriteLine("Object UploadID: {0}", upload.UploadID);
                        Console.WriteLine("Object Owner: {0}", upload.Owner);
                        Console.WriteLine("Object StorageClass: {0}", upload.StorageClass);
                    }

                    truncated = listMultipartUploadsOutput.IsTruncated;
                    marker = listMultipartUploadsOutput.NextKeyMarker;
                }
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("ListMultipartUploads failed, request id {0}", ex.RequestID);
                Console.WriteLine("ListMultipartUploads failed, status code {0}", ex.StatusCode);
                Console.WriteLine("ListMultipartUploads failed, response error code {0}", ex.Code);
                Console.WriteLine("ListMultipartUploads failed, response error message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("ListMultipartUploads failed, error message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("ListMultipartUploads failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed description of the API for listing multipart uploads, see [ListMultipartUploads](https://docs.byteplus.com/docs/tos/reference-listmultipartuploads).
