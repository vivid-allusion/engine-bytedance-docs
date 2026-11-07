---
title: "Managing Object Tags (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-labels-c-sdk"
---

TOS supports assigning tags to objects and performs lifecycle management for specific objects based on their tags. This article introduces the relevant parameters of object tags and management objects.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* To set object tags, you must have the `tos:PutObjectTagging` permission. For specific instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To retrieve object tags, you must have the `tos:GetObjectTagging` permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* To delete object tags, you must have the `tos:DeleteObjectTagging` permission. For detailed instructions, please refer to the [Permission configuration guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* A maximum of 10 tags can be added to each object, and tag keys on the same object must be unique. For details regarding object tag restrictions, please refer to [Object tag restrictions](https://docs.byteplus.com/docs/tos/docs-managing-file-labels).


<span id=".6K6-572u5a-56LGh5qCH562-"></span>
## Configure object tags

TOS supports categorizing objects within a bucket using tags, and allows you to configure lifecycle rules for objects with the same tags.

The following code is used to set object tags.

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

    
    PutObjectTaggingInput input(bucketName, objectName);
   
    Tag tag1("key1","value1");
    Tag tag2("key2","value2");
    TagSet tagSet({tag1,tag2});
    input.setTagSet(tagSet);
    auto output = client.putObjectTagging(input);
    if (!output.isSuccess()) {
        
        std::cout << "PutObjectTagging failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }

    std::cout << "PutObjectTagging success." << std::endl;

    CloseClient();
    return 0;
}
```


<span id=".6I635Y-W5a-56LGh5qCH562-"></span>
## Retrieve object tags

After setting object tags, you can retrieve the tag information of an object as needed. When versioning is enabled for a bucket, TOS returns the tag information of the current version of the object by default. You can obtain the tag information of a specific version by specifying the object's version.

The following code is used to obtain the object tag information for `exampledir/exampleobject.txt` in the bucket `examplebucket`.

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


    GetObjectTaggingInput input(bucketName, objectName);
    auto output = client.getObjectTagging(input);
    if (!output.isSuccess()) {
     
        std::cout << "GetObjectTagging failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }

    std::cout << "GetObjectTagging success." << std::endl;
    for(auto& tag : output.result().getTagSet().getTags()){
        std::cout << " tag key is:" << tag.getKey()
                  << " tag value is:" <<  tag.getValue() << std::endl;
    }

    CloseClient();
    return 0;
}
```


<span id=".5Yig6Zmk5a-56LGh5qCH562-"></span>
## Delete object tags

You may delete any unnecessary tag information as required. When versioning is enabled for a bucket, TOS deletes only the tags of the current version of an object by default. You can delete the tags of a specific version by specifying the object's version ID.

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


    DeleteObjectTaggingInput input(bucketName, objectName);
    auto output = client.deleteObjectTagging(input);
    if (!output.isSuccess()) {
      
        std::cout << "DeleteObjectTagging failed." << output.error().String() << std::endl;
    
        CloseClient();
        return -1;
    }

    std::cout << "DeleteObjectTagging success." << std::endl;
  
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant documentation**

For more information about object tags, see [Manage object tags](https://docs.byteplus.com/docs/tos/docs-managing-file-labels).
