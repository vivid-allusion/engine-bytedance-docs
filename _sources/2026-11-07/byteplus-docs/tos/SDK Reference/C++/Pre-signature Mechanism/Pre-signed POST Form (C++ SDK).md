---
title: "Pre-signed POST Form (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Post-form-Presignature-c-sdk"
---

TOS supports browser\-based POST object upload requests, enabling you to upload content directly to TOS. When uploading an object using POST, you must include signature information in the form.

<span id=".5YyF5ZCr5Z-656GA5Y-C5pWw55qELXBvc3Qt6KGo5Y2V6aKE562-5ZCN"></span>
## **Pre\-signed POST form with basic parameters**

The following code is used for POST form\-based pre\-signed object uploads that include only basic parameters.

```cpp
#include "TosClientV2.h"

using namespace VolcengineTos;

int main(void)
{
   
   
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
   
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.txt";
    
   
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);
    
    
    int64_t expires = 86400;
    
    PreSignedPostSignatureInput input(bucketName,objectName, expires);
    auto output = client.preSignedPostSignature(input);
    if(!output.isSuccess()){
        
        std::cout << "GeneratePreSignedUrl failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }

    auto res = output.result();
    std::cout << "GeneratePreSignedUrl Success:" << "\n"
              << "Policy: " << res.getPolicy() << "\n"
              << "Algorithm: " << res.getAlgorithm() << "\n"
              << "Credential: " << res.getCredential() << "\n"
              << "Date: " << res.getDate() << "\n"
              << "OriginPolicy: " << res.getOriginPolicy() << "\n"
              << "Signature: " << res.getSignature() << "\n";
  
    CloseClient();
    return 0;

}
```


<span id=".5YyF5ZCr5aSa5Liq6KGo5Y2V5Z-f55qEcG9zdOmihOetvuWQjQ=="></span>
## **Pre\-signed POST with multiple form fields**

The following code is an example of uploading objects with multiple form fields.

```cpp
#include "TosClientV2.h"

using namespace VolcengineTos;

int main(void)
{
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
  
    std::string bucketName = "examplebucket";
  
    std::string objectName = "exampledir/exampleobject.txt";
    
 
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);
    

    int64_t expires = 86400;

    PreSignedPostSignatureInput input(bucketName,objectName, expires);

    input.setConditions(
            {PostSignatureCondition("x-tos-acl", "public-read"),
             PostSignatureCondition("key", "sdktest", std::make_shared<std::string>("starts-with"))});
 
    input.setContentLengthRange(std::make_shared<ContentLengthRange>(50, 1025));
    auto output = client.preSignedPostSignature(input);
    if(!output.isSuccess()){
  
        std::cout << "GeneratePreSignedUrl failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }

    auto res = output.result();
    std::cout << "GeneratePreSignedUrl Success:" << "\n"
              << "Policy: " << res.getPolicy() << "\n"
              << "Algorithm: " << res.getAlgorithm() << "\n"
              << "Credential: " << res.getCredential() << "\n"
              << "Date: " << res.getDate() << "\n"
              << "OriginPolicy: " << res.getOriginPolicy() << "\n"
              << "Signature: " << res.getSignature() << "\n";
  
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For detailed information about POST form presigning, see [Including a signature in browser-based upload forms](https://docs.byteplus.com/docs/tos/reference-browser-based-upload-forms-include-signatures).
