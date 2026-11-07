---
title: "Video Frame Extraction (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-framing-c-sdk"
---

The video frame extraction function enables the capture of a single frame from a video stream at a specified time and resizes it into an image of designated dimensions. This article explains how to perform video frame capture using the TOS C++ SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to extract the video frame at 300 milliseconds, name the extracted image temp.jpg, and download it to the local computer.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    std::string objectName = "exampledir/exampleobject.mp4";
    
    std::string filePath = "/localpath/temp.jpg";
    
    
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);
    
    GetObjectToFileInput input(bucketName, objectName, filePath);
    std::string style = "video/snapshot,t_300";
    input.setProcess(style);
    auto output = client.getObjectToFile(input);
    if (!output.isSuccess()) {
        
        std::cout << "GetObjectToFile failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }
    
    std::cout << "GetObjectToFile success. the object etag:" << output.result().getGetObjectBasicOutput().getETags()
              << std::endl;
    
   
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to video frame capture, please refer to [Video Frame Capture](https://docs.byteplus.com/docs/tos/docs-video-frame-capture).
