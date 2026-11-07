---
title: "Restore Object (.Net SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Restore-objects-net-sdk"
---

Restore a Cold Archive object; after restoration, the object can be obtained through the download object interface. Different retrieval methods can be specified through parameters.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* The first invocation of the RestoreObject API returns a 202 status code. If a file is currently being restored, invoking the RestoreObject API again will return a 409 error. If the object has already been restored, invoking the RestoreObject API again will return a 200 OK response.

* For buckets with versioning enabled, you can restore a specific version of an object by specifying the VersionId. If VersionId is not specified, the current version of the object will be restored by default.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to restore objects.

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
                var restoreObjectInput = new RestoreObjectInput
                {
                    Bucket = bucketName,
                    Key = objectKey,
                    Days = 1,
                    VersionID = "",
                };

                var restoreObjectOutput = client.RestoreObject(restoreObjectInput);
                Console.WriteLine("RestoreObject succeeded, Request ID {0}", restoreObjectOutput.RequestID);
            }
            catch (TosServerException ex)
            {
                Console.WriteLine("RestoreObject failed, Request ID {0}", ex.RequestID);
                Console.WriteLine("RestoreObject failed, Status Code {0}", ex.StatusCode);
                Console.WriteLine("RestoreObject failed, Response Error Code {0}", ex.Code);
                Console.WriteLine("RestoreObject failed, Response Error Message {0}", ex.Message);
            }
            catch (TosClientException ex)
            {
                Console.WriteLine("RestoreObject failed, Error Message {0}", ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine("RestoreObject failed, {0}", ex.Message);
            }
        }
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For a detailed introduction to the Restore Object interface, see [RestoreObject](https://docs.byteplus.com/docs/tos/reference-restoreobject).
