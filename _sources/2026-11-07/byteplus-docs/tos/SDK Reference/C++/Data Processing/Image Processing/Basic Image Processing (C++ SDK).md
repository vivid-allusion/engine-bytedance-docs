---
title: "Basic Image Processing (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Basic-image-processing-c-sdk"
---

TOS supports processing of stored images, including image resizing, image cropping, image watermarking, format conversion, and other image processing operations. This article explains how to use the TOS C++ SDK for basic image processing.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The supported formats for original images are limited to JPG, PNG, BMP, GIF, WEBP, and TIFF.

* The original image size must not exceed 20MB.

* The original image width and height must not exceed 30,000 px, and the total pixel count must not exceed 250 million px. For rotation operations, the original image width and height must not exceed 4,096 px.

* The width and height of the scaled image must not exceed 16,384 px, and the total number of pixels must not exceed 16,777,216 px.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to fix the image height at 100px, convert the image format to JPG, rename the image as temp.jpg, and download it to the local computer.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
  

    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "examplebucket";
 
    std::string objectName = "exampledir/exampleobject.jpg";
 
    std::string filePath = "/localpath/temp.jpg";
    
  
    InitializeClient();
  
    TosClientV2 client(region, accessKey, secretKey);
    
    GetObjectToFileInput input(bucketName, objectName, filePath);
    std::string style = "image/resize,h_100/format,jpg";
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

For a detailed introduction to image processing, please refer to [Image Processing Overview](https://docs.byteplus.com/docs/tos/docs-overview_2).
