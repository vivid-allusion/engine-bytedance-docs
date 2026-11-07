---
title: "Standard Pre-signed (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-pre-signature-c-sdk"
---

By default, TosClient includes a signature in the request header when initiating a request to the server. The SDK also supports generating signed URLs, which can be used directly to initiate HTTP requests or shared with third parties to enable access authorization. This document uses uploading and downloading objects via pre\-signed URLs as examples. If you have other requirements, you may refer to the settings described herein.

<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIrkvKDlr7nosaE="></span>
## **Uploading Objects Using Pre\-Signed URLs**

Generate a sample pre\-signed URL for uploading.

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
   
    PreSignedURLInput input(HttpMethodType::Put,bucketName,objectName,expires);
  
    // input.setAlternativeEndpoint("Your Alternative Endpoint");
    input.set
    auto output = client.preSignedURL(input);
    if(!output.isSuccess()){
      
    std::cout << "GeneratePreSignedUrl failed." << output.error().String() << std::endl;

    CloseClient();
        return -1;
    }

    std::cout << "GeneratePreSignedUrl Success, Gen Url:"<< output.result().getSignUrl() << std::endl;

    CloseClient();
    return 0;
}

// http://examplebucket.{endpoint/host}/exampledir/exampleobject.txt?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential={xxx}/{date}/{region}/tos/request&X-Tos-Date=20220922T103306Z&X-Tos-Expires=86400&X-Tos-Signature={yyy}&X-Tos-SignedHeaders=host
```


<span id=".5L2_55So6aKE562-5ZCN55qELXVybC3kuIvovb3lr7nosaE="></span>
## **Downloading Objects Using Pre\-Signed URLs**

Generate a sample pre\-signed URL for download.

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

    PreSignedURLInput input(HttpMethodType::Get,bucketName,objectName,expires);
    auto output = client.preSignedURL(input);
    if(!output.isSuccess()){
  
    std::cout << "GeneratePreSignedUrl failed." << output.error().String() << std::endl;
     
    CloseClient();
        return -1;
    }

    std::cout << "GeneratePreSignedUrl Success, Gen Url:"<< output.result().getSignUrl() << std::endl;
  
    CloseClient();
    return 0;
}

// http://examplebucket.{endpoint/host}/exampledir/exampleobject.txt?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential={xxx}/{date}/{region}/tos/request&X-Tos-Date=20220922T103306Z&X-Tos-Expires=86400&X-Tos-Signature={yyy}&X-Tos-SignedHeaders=host
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For detailed information about URLs containing signatures, see [URLs Containing Signatures](https://docs.byteplus.com/docs/tos/reference-including-a-signature-in-the-url).
