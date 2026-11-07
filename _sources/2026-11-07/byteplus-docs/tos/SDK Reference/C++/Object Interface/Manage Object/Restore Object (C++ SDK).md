---
title: "Restore Object (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Restore-objects-c-sdk"
---

Restore cold archive objects; after restoration, the objects can be obtained via the download object interface. Different retrieval methods can be specified through parameters.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When the restoreObject interface is called for the first time, a 202 status code is returned. If a file is in the process of being restored, invoking the restoreObject interface again will result in a 409 error. If the object has already been restored, invoking the restoreObject API again will return a 200 OK response.

* For buckets with versioning enabled, you can restore a specific version of an object by specifying the versionId. If versionId is not specified, the current version of the object will be restored by default.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code is used to restore objects.

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
    
    RestoreObjectInput input(bucketName, objectName, 10, RestoreJobParameters(TierType::TierExpedited));
    auto output = client.restoreObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "RestoreObject failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }
    std::cout << "RestoreObject success." << std::endl;
    
  
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to the Restore Object API, see [RestoreObject](https://docs.byteplus.com/docs/tos/reference-restoreobject).
