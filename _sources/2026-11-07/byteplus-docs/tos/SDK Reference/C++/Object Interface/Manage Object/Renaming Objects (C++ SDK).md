---
title: "Renaming Objects (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Rename-objects-c-sdk"
---

TOS supports renaming the key of an individual object within a bucket without copying or deleting data.

<span id="432dfc50"></span>
## **Precautions**


* Before renaming an object, you must first enable the renaming feature.

* Renaming is supported only for objects uploaded after the RenameObject feature is enabled; it is not supported for objects that existed prior to enabling this feature.

* Concurrent renaming is not supported for the same object.

* All information contained in the metadata of the renamed object is identical to that of the source object.


<span id="8b90ebc9"></span>
## **Sample Code**

The following code is used for the object renaming functionality.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
 
 
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
   
    std::string bucketName = "examplebucket";
 
    std::string objectName = "exampledir/exampleobject1.txt";
    std::string objectNameNew = "exampledir/exampleobject2.txt";
    
    
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);
    

    PutBucketRenameInput input(bucketName, true);
    auto output = client.putBucketRename(input);
    if (!output.isSuccess()) {
 
        std::cout << "PutBucketRename failed." << output.error().String() << std::endl;

        CloseClient();
        return -1;
    }
    std::cout << "PutBucketRename success." << std::endl;
    
    RenameObjectInput renameInput(bucketName, objectName, objectNameNew);
    auto renameOutput = client.renameObject(renameInput);
    if (!renameOutput.isSuccess()) {
     
        std::cout << "RenameObject failed." << renameOutput.error().String() << std::endl;

        CloseClient();
        return -1;
    }
    std::cout << "RenameObject success." << std::endl;
    

    CloseClient();
    return 0;
}
```


<span id="a6c81025"></span>
## Reference Document

For the API documentation on RenameObject, see [RenameObject](https://docs.byteplus.com/docs/tos/Renameobject).
