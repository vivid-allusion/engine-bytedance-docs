---
title: "Pre-signed URL (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Presigned-urls-net-sdk"
---

By default, TosClient includes a signature in the request header when sending a request to the server. The SDK also supports generating signed URLs, which users can use directly to initiate HTTP requests or share with third parties to grant access authorization. This article presents SDK examples for pre\-signed URLs.

<span id=".5L2_55So6aKE562-5ZCNLXVybC3kuIrkvKDlr7nosaE="></span>
## Uploading Objects Using Pre\-Signed URLs

The following code is used to generate a pre\-signed URL, which is then utilized to upload an object to the specified bucket.

```C#
using System;
using System.Collections.Generic;
using System.IO;
using System.Net;
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
            var data = "Hello TOS";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var preSignedURLInput = new PreSignedURLInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    HttpMethod = HttpMethodType.HttpMethodPut,
                    Header = new Dictionary<string, string>() { { "Content-Type", "text/plain" } }
                };
                var preSignedURLOutput = client.PreSignedURL(preSignedURLInput);

                HttpWebRequest request = (HttpWebRequest)WebRequest.Create(preSignedURLOutput.SignedUrl);
                request.Method = WebRequestMethods.Http.Put;
                var body = System.Text.Encoding.UTF8.GetBytes(data);
                request.ContentLength = data.Length;
                request.ContentType = "text/plain";
                using (Stream requestStream = request.GetRequestStream())
                {
                    requestStream.Write(body, 0, data.Length);
                }

                HttpWebResponse response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine("PreSignedURL Put Object Status Code {0}", response.StatusCode);
                response.Close();
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("PreSignedURL failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("PreSignedURL failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("PreSignedURL failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("PreSignedURL failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("PreSignedURL failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("PreSignedURL failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIvovb3lr7nosaE="></span>
## Downloading Objects Using Pre\-Signed URLs

The following code is used to generate a pre\-signed URL, which is then used to download an object from the specified bucket.

```C#
using System;
using System.Net;
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
            var data = "Hello TOS";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var preSignedURLInput = new PreSignedURLInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    HttpMethod = HttpMethodType.HttpMethodGet,
                };
                var preSignedURLOutput = client.PreSignedURL(preSignedURLInput);

                var request = (HttpWebRequest)WebRequest.Create(preSignedURLOutput.SignedUrl);
                request.Method = WebRequestMethods.Http.Get;
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine("PreSignedURL Get Object Status Code {0}", response.StatusCode);
                response.Close();
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("PreSignedURL failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("PreSignedURL failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("PreSignedURL failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("PreSignedURL failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("PreSignedURL failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("PreSignedURL failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3liKDpmaTlr7nosaE="></span>
## Deleting Objects Using Pre\-Signed URLs

The following code generates a pre\-signed URL, which is then used to delete an object from the specified bucket.

```C#
using System;
using System.Net;
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
            var data = "Hello TOS";

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var preSignedURLInput = new PreSignedURLInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    HttpMethod = HttpMethodType.HttpMethodDelete,
                };
                var preSignedURLOutput = client.PreSignedURL(preSignedURLInput);

                var request = (HttpWebRequest)WebRequest.Create(preSignedURLOutput.SignedUrl);
                request.Method = "DELETE";
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine("PreSignedURL Delete Object Status Code {0}", response.StatusCode);
                response.Close();
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("PreSignedURL failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("PreSignedURL failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("PreSignedURL failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("PreSignedURL failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("PreSignedURL failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("PreSignedURL failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For detailed information about URLs containing signatures, see [URLs Containing Signatures](https://docs.byteplus.com/docs/tos/reference-including-a-signature-in-the-url).
