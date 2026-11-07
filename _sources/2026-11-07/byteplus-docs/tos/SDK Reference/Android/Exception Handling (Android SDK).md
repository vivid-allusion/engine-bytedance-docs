---
title: "Exception Handling (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Exception-handling-android-sdk"
---

Requests are sent to the TOS server via the TOS Android SDK interface. The response to each request includes a return code, which identifies the status of the current operation. TOS services comply with the HTTP specification.

<span id=".dG9zLeacjeWKoeerr-mUmeivrw=="></span>
## TOS Server\-Side Error

The TOS server adheres to HTTP standards and defines detailed HTTP status codes and business error codes for scenarios involving request failures. For detailed information, please refer to [Definition of TOS Server Status Codes and Error Codes](https://docs.byteplus.com/en/docs/tos/reference-codes-in-response).

<span id=".c2RrLeiHquWumuS5ieW8guW4uC3plJnor68="></span>
## SDK Custom Exceptions and Errors

Catch TosException and retrieve the error code (Code), HTTP status code (StatusCode), and other relevant information. The following is a sample code.

```java

try{
/* your code */
} catch(TosException e){
    /**
    * 
    **/
    Log.e("TosException", e.getCode()); 
    
    /**
    * 
    **/
    Log.e("TosException", e.getStatusCode()); 
    
    Log.e("TosException", e.toString()); 
}


try{
/* your code */
} catch(TosServerException e){
  
    Log.e("TosException", e.getCode()); 
    
    Log.e("TosException", e.getStatusCode()); 
} catch(TosClientException e){
    Log.e("TosException", e.toString()) 
} catch(TosException e) {
    Log.e("TosException", e.toString()) 
}
```
