---
title: "Abnormal Image Detection (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/abnormal-image-detection-c-sdk"
---

Anomalous image detection is used to identify whether an image contains suspicious files other than the image itself, such as MPEG\-TS files. If an image is detected to contain suspicious files, you may process the image file to prevent the storage space from being misappropriated by illicit image hosting services. This article describes how to use the TOS C++ SDK to perform anomaly image detection.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The size of the original image for detection must not exceed 20 MB.

* Anomaly image detection is supported only for files in JPG, JPEG, PNG, BMP, GIF, and pure TS video stream formats.

* The abnormal image detection function is billed based on the number of processing operations. For detailed information, please refer to [Data Processing Fees](https://docs.byteplus.com/docs/tos/docs-data-processing-fee).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to detect anomalous images.

```go
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
    std::string style = "image/inspect";
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

For a detailed introduction to anomalous image detection, please refer to [Anomalous Image Detection](https://docs.byteplus.com/docs/6349/1140988).
