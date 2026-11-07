---
title: "Append Upload (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-c-sdk"
---

The object type created during append upload is an appendable object (Appendable Object), which allows data to be appended to the end of the object. Objects created through standard upload and multipart upload are of the Normal Object type. Data cannot be appended to these objects.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before appending to an object, you must have the `tos:PutObject` permission. For specific operations, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* When uploading an object, the object name must comply with specific standards. For detailed information, please refer to [Object Naming Guidelines](https://docs.byteplus.com/docs/tos/docs-common-concepts).

* TOS is a distributed object storage product designed for large\-scale storage, with internal partitions that store object index data. To enable horizontal scaling and maximize the throughput of object uploads and downloads, as well as to reduce the likelihood of hotspot partitions, please avoid using lexicographically incremental object naming. For more information, see [Performance Optimization](https://docs.byteplus.com/docs/tos/Performance-optimization-plan).

* If an object with the same name already exists in the bucket, the new object will overwrite the existing one. When bucket versioning is enabled, the original object is retained, and a new version ID is generated to identify the newly uploaded object.

* Append upload operations do not support requests using Chunk\-Encoded transfer encoding. When performing append uploads for network streams, please retrieve data iteratively and then append it.


<span id=".6L-95Yqg5LiK5Lyg6ZmQ5Yi2"></span>
## Additional Upload Restrictions

The object size limitations when using the appendObject interface are as follows:


* The size of the object after appending must not exceed 5 GiB.

* When an object created using appendObject is subjected to a putObject operation, the object is overwritten and its type changes from Appendable to Normal. Conversely, objects uploaded via putObject do not support append write operations.

* Objects created by appendObject do not support copying.

* The appendObject interface cannot be used if the object type is Infrequent Access Storage or Archive Flashback Storage.

* If your storage bucket is in a state where multi\-version control is enabled or suspended, the appendObject interface cannot be used.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

<span id=".5LuO5YaF5a2Y5Lit6L-95Yqg5LiK5Lyg"></span>
### **Upload additional data from memory**

The following code is used to append and upload a string from memory to the `exampledir/exampleobject.txt` object in the target bucket `examplebucket`.

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

    
    auto part0 = std::make_shared<std::stringstream>();
    for (int i = 0; i < (128 << 10); ++i) {
        *part0 << "1";
    }
    AppendObjectV2Input input(bucketName, objectName, part0, 0);
    auto output = client.appendObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "AppendObject failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    std::cout << "AppendObject success." << std::endl;
    std::cout << "Next Append Offset is: " << output.result().getNextAppendOffset() << std::endl;
    std::cout << "Pre HashCrc64Ecma is: " << output.result().getHashCrc64ecma() << std::endl;


    auto part1 = std::make_shared<std::stringstream>();
    for (int i = 0; i < (256 << 10); ++i) {
        *part1 << "1";
    }
    input.setContent(part1);
    
    input.setOffset(output.result().getNextAppendOffset());
    input.setPreHashCrc64Ecma(output.result().getHashCrc64ecma());
    auto output1 = client.appendObject(input);
    if (!output.isSuccess()) {
        
        std::cout << "AppendObject failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "AppendObject success." << std::endl;
    std::cout << "Next Append Offset is: " << output1.result().getNextAppendOffset() << std::endl;
    std::cout << "Pre HashCrc64Ecma is: " << output1.result().getHashCrc64ecma() << std::endl;

   
    CloseClient();
    return 0;
}
```


<span id=".6L-b5bqm5p2h5aSE55CG"></span>
### **Progress Bar Handling**

The following code is used to add a progress bar feature to the append upload process.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

static void ProgressCallback(std::shared_ptr<DataTransferStatus> datatransferstatus) {
    int64_t consumedBytes = datatransferstatus->consumedBytes_;
    int64_t totalBytes = datatransferstatus->totalBytes_;
    int64_t rwOnceBytes = datatransferstatus->rwOnceBytes_;
    DataTransferType type = datatransferstatus->type_;
    int64_t rate = 100 * consumedBytes / totalBytes;
    std::cout << "rate:" << rate << ","
              << "ConsumedBytes:" << consumedBytes << ","
              << "totalBytes:" << totalBytes << ","
              << "rwOnceBytes:" << rwOnceBytes << ","
              << "DataTransferType:" << type << std::endl;
}

int main(void){
  
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";

    std::string objectName = "exampledir/exampleobject.txt";


    InitializeClient();
  
    TosClientV2 client(region, accessKey, secretKey);

  
    auto part0 = std::make_shared<std::stringstream>();
    for (int i = 0; i < (128 << 10); ++i) {
        *part0 << "1";
    }
    AppendObjectV2Input input(bucketName, objectName, part0, 0);

   
    DataTransferListener datatransferlistener = {ProgressCallback, nullptr};
    input.setDataTransferListener(datatransferlistener);

    auto output = client.appendObject(input);
    if (!output.isSuccess()) {
      
        std::cout << "AppendObject failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }
    std::cout << "AppendObject success." << std::endl;
    std::cout << "Next Append Offset is: " << output.result().getNextAppendOffset() << std::endl;
    std::cout << "Pre HashCrc64Ecma is: " << output.result().getHashCrc64ecma() << std::endl;


    auto part1 = std::make_shared<std::stringstream>();
    for (int i = 0; i < (256 << 10); ++i) {
        *part1 << "1";
    }
    input.setContent(part1);
 
    input.setOffset(output.result().getNextAppendOffset());
    input.setPreHashCrc64Ecma(output.result().getHashCrc64ecma());
    auto output1 = client.appendObject(input);
    if (!output.isSuccess()) {
       
        std::cout << "AppendObject failed." << output.error().String() << std::endl;
    
        CloseClient();
        return -1;
    }
    std::cout << "AppendObject success." << std::endl;
    std::cout << "Next Append Offset is: " << output1.result().getNextAppendOffset() << std::endl;
    std::cout << "Pre HashCrc64Ecma is: " << output1.result().getHashCrc64ecma() << std::endl;

 
    CloseClient();
    return 0;
}
```


<span id=".5a6i5oi356uv6ZmQ6YCf"></span>
### **Client\-Side Rate Limiting**

The following code is used to configure client\-side rate limiting during the append upload process.

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


    auto part0 = std::make_shared<std::stringstream>();
    for (int i = 0; i < (128 << 10); ++i) {
        *part0 << "1";
    }
    AppendObjectV2Input input(bucketName, objectName, part0, 0);

    
    std::shared_ptr<RateLimiter> RateLimiter(NewRateLimiter(1024 * 1024, 1024 * 1024));
    input.setRateLimiter(RateLimiter);

    auto output = client.appendObject(input);
    if (!output.isSuccess()) {
    
        std::cout << "AppendObject failed." << output.error().String() << std::endl;
 
        CloseClient();
        return -1;
    }
    std::cout << "AppendObject success." << std::endl;
    std::cout << "Next Append Offset is: " << output.result().getNextAppendOffset() << std::endl;
    std::cout << "Pre HashCrc64Ecma is: " << output.result().getHashCrc64ecma() << std::endl;


    auto part1 = std::make_shared<std::stringstream>();
    for (int i = 0; i < (256 << 10); ++i) {
        *part1 << "1";
    }
    input.setContent(part1);

    input.setOffset(output.result().getNextAppendOffset());
    input.setPreHashCrc64Ecma(output.result().getHashCrc64ecma());
    auto output1 = client.appendObject(input);
    if (!output.isSuccess()) {
     
        std::cout << "AppendObject failed." << output.error().String() << std::endl;

        CloseClient();
        return -1;
    }
    std::cout << "AppendObject success." << std::endl;
    std::cout << "Next Append Offset is: " << output1.result().getNextAppendOffset() << std::endl;
    std::cout << "Pre HashCrc64Ecma is: " << output1.result().getHashCrc64ecma() << std::endl;

 
    CloseClient();
    return 0;
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documents**

For documentation on the append upload API, please refer to [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject).
