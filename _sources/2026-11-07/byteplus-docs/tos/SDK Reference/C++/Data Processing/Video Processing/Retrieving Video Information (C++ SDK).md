---
title: "Retrieving Video Information (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-video-information-c-sdk"
---

The video information retrieval function enables the acquisition of metadata for a specified video resource. This document describes how to obtain video information using the TOS C++ SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to retrieve video information.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.mp4";
    
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);
    
    GetObjectV2Input input(bucketName, objectName);
    std::string style = "video/info";
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

For detailed information on how to obtain video details, please refer to [Viewing Video Information](https://docs.byteplus.com/docs/tos/docs-viewing-video-information).
