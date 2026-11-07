---
title: "Retrieving Image Information (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-image-information-c-sdk"
---

The image information retrieval function provides access to the basic attributes of an image, including its height, width, size, and format. If the image contains Exif information, the content will be returned in JSON format. This article describes how to obtain image information using the TOS C++ SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to retrieve image information.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){

    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.jpg";
    
    
    InitializeClient();
   
    TosClientV2 client(region, accessKey, secretKey);
    
    GetObjectV2Input input(bucketName, objectName);
    std::string style = "image/info";
    input.setProcess(style);
    auto output = client.getObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "GetObjectToFile failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    
    std::ostringstream ss;
    ss << output.result().getContent()->rdbuf();
  
    std::string infoJson = ss.str();
    

    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to obtaining image information, please refer to [Obtain Image Information](https://docs.byteplus.com/docs/tos/docs-information-query).
