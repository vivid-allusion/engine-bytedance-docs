---
title: "Exception Handling (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Exception-handling-c-sdk"
---

This document describes exception handling when using the TOS SDK.

<span id=".dG9zLeacjeWKoeerr-mUmeivrw=="></span>
## TOS Server\-Side Error

The TOS server adheres to HTTP specifications and defines detailed HTTP status codes and business error codes for scenarios involving request failures. For detailed information, please refer to [Definition of TOS server-side status codes and error codes](https://docs.byteplus.com/en/docs/tos/reference-codes-in-response).

<span id=".c2RrLeiHquWumuS5ieW8gumUmeivrw=="></span>
## Custom Exception Handling in SDK

<span id=".5a6i5oi356uv6ZSZ6K-v"></span>
### Client Error

Client errors are reported in scenarios such as when incorrect input parameters are provided, or when errors occur that require canceling resumable uploads and similar operations. For example, when creating a bucket, if the bucket name exceeds 63 characters in length, the returned error will have the isClientError parameter set to true, indicating that a client\-side error has occurred.

<span id=".5pyN5Yqh56uv6ZSZ6K-v"></span>
### Server\-side Error

When a request is sent to the TOS server via the TOS C++ SDK interface, the response includes status codes that comply with HTTP standards as well as business error codes, which indicate the response status of the current request. At the same time, the value of the isClientError parameter is false.

<span id=".6ZSZ6K-v5aSE55CG56S65L6L"></span>
### Error Handling Examples

The following code demonstrates how to download an object and handle the return values on the client side. In the event of a server\-side error, you can print the HTTP request status code, error message, RequestId, and HostId. If a client\-side error occurs, you can print the error message.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
 
  
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
  
    std::string objectName = "exampledir/exampleobject.txt";

    
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey);

    GetObjectV2Input input(bucketName, objectName);
    auto output = client.getObject(input);
    if (!output.isSuccess()) {
        auto error = output.error();
        if(error.isClientError()){
            
            std::cout << "TosClientError: {message=" << error.getMessage() << "}";
        } else {
       
            std::cout << "TosServerError: {statusCode=" << error.getStatusCode() << ", "
            << "code=" << error.getCode() << ", "
            << "message=" << error.getMessage() << ", "
            << "requestID=" << error.getRequestId() << ", "
            << "hostID=" << error.getHostId() << "}";
        }
     
        CloseClient();
        return -1;
    }

    std::cout << "GetObject success. the object etag:" << output.result().getETags()  << std::endl;
  
    CloseClient();
    return 0;
}
```
