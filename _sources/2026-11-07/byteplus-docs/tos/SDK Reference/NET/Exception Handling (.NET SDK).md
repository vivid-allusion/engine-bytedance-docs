---
title: "Exception Handling (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Exception-handling-net-sdk"
---

This document describes exception handling when using the TOS SDK.

<span id=".dG9zLeacjeWKoeerr-mUmeivrw=="></span>
## TOS Server\-Side Error

The TOS server complies with HTTP standards and specifies detailed HTTP status codes and business error codes for scenarios involving request failures. For detailed information, please refer to [Definition of TOS Server Status Codes and Error Codes](https://docs.byteplus.com/docs/6349/74874).

<span id=".c2RrLeiHquWumuS5ieW8guW4uA=="></span>
## SDK Custom Exceptions

<span id=".5a6i5oi356uv5byC5bi4LXRvc2NsaWVudGVycm9y"></span>
### Client Error \- TosClientError

TosClientError is caused by client input parameter errors, connection timeouts, or special client operations such as canceling resumable upload processes and other similar special operations. For example, when using CreateBucket to create a bucket, an exception is returned if the bucket name exceeds 63 characters in length.

<span id=".5pyN5Yqh56uv5byC5bi4LXRvc3NlcnZlcmVycm9y"></span>
### Server\-Side Exception \- TosServerError

Requests are sent to the TOS server via the TOS .NET SDK interface. The response to each request includes status codes that comply with HTTP standards, as well as business error codes, which together indicate the response status of the current request.

<span id=".5byC5bi45aSE55CG56S65L6L"></span>
### Exception Handling Examples

The following code demonstrates exception handling when attempting to download a non\-existent object. If a TosServerError exception occurs, the exception message, HTTP request status code, and request ID are printed. If a TosClientError exception occurs, the exception message and the underlying cause of the error are printed.

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

            var client = TosClientBuilder.Builder().SetAk(ak).SetSk(sk).SetEndpoint(endpoint).SetRegion(region).Build();

            try
            {
                var getObjectInput = new GetObjectInput()
                {
                    Bucket = bucketName,
                    Key = objectKey,
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
                if (ex.StatusCode == 404)
                {
                    Console.WriteLine("GetObject failed, object not exist");
                }

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
