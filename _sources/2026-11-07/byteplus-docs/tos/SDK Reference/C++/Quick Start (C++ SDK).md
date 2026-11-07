---
title: "Quick Start (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start-c-sdk"
---

This article describes how to perform basic operations using the TOS C++ SDK, such as creating buckets, uploading, downloading, and deleting objects.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Install SDK](https://docs.byteplus.com/docs/tos/Install-c-sdk)

2. [Initialize Client](https://docs.byteplus.com/docs/tos/Initialize-client-side-c-sdk)


<span id=".5a6i5oi356uv6YCa55So56S65L6L"></span>
## General Client Example

Describe the general usage of TosClient through a sample code template.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
    

    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");

    std::string bucketName = "examplebucket";
  
    InitializeClient();

    TosClientV2 client(region, accessKey, secretKey);
        CreateBucketV2Input input(bucketName);     
    auto output = client.createBucket(input);
    if(!output.isSuccess()){
        auto error = output.error();
        if(error.isClientError()){
       
            std::cout << "TosClientError: {message=" << error.getMessage() << "}";
        } else {
       
            std::cout << "TosServerError: {statusCode=" << error.getStatusCode() << ", "
            << "code=" << error.getCode() << ", "
            << "message=" << error.getMessage() << ", "
            << "requestID=" << error.getRequestId() << ", "
            << "hostID=" << error.getHostId() << "}";
        }
        CloseClient();
        return -1;
    } 
    
    std::cout << "CreateBucket Success, the Bucket Location:"<< output.result().getLocation() << std::endl;
 
    CloseClient();
    return 0;
}
```


<span id=".5Yib5bu65qG2"></span>
## Creating a Bucket

A Bucket is the globally unique namespace in TOS, functioning as a data container for storing object data. The following code demonstrates how to create a new bucket.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){

 
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
   
    std::string bucketName = "examplebucket";
      
    InitializeClient();
    
    TosClientV2 client(region, accessKey, secretKey);
        CreateBucketV2Input input(bucketName);    
    auto output = client.createBucket(input);
    if (!output.isSuccess()) {
      
        std::cout << "CreateBucket failed." << output.error().String() << std::endl;
     
        CloseClient();
        return -1;
    }

    std::cout << "CreateBucket Success, the bucket location:" << output.result().getLocation() << std::endl;


    CloseClient();
    return 0;
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about creating buckets, see <a href="https://docs.byteplus.com/docs/tos/Create-bucket-c-sdk">Creating Buckets</a>.</div>


<span id=".5LiK5Lyg5a-56LGh"></span>
## Upload Object

After a bucket is successfully created, objects can be uploaded to the bucket. The following code demonstrates how to upload a string to an existing bucket.

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
    
    
    std::string data = "Object data to be uploaded";
    auto ss = std::make_shared<std::stringstream>(data);
    PutObjectV2Input input(bucketName, objectName, ss);
    auto output = client.putObject(input);
    if (!output.isSuccess()) {
       
    std::cout << "PutObject failed." << output.error().String() << std::endl;
     
    CloseClient();
        return -1;
    }

    std::cout << "PutObject success. the object etag:" << output.result().getETag() << std::endl;
   
    CloseClient();
    return 0;
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example links on uploading objects, see <a href="https://docs.byteplus.com/docs/tos/Normal-upload-c-sdk">Uploading Objects</a>.</div>


<span id=".5LiL6L295a-56LGh"></span>
## Download Object

The following code is used to download the specified object into memory.

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
    
    GetObjectV2Input input(bucketName, objectName);
    auto output = client.getObject(input);
    if (!output.isSuccess()) {
       
        std::cout << "GetObject failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }
    auto stream = output.result().getContent();
    std::string ss;;

    char streamBuffer[256];
    memset(streamBuffer, 0, 256);
    while (stream->good()) {
        stream->read(streamBuffer, 256);
       
    }
    std::cout << "GetObject success. the object etag:" << output.result().getETags()  << std::endl;

    
    CloseClient();
    return 0;
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more example links regarding download objects, see <a href="https://docs.byteplus.com/docs/tos/Normal-download-c-sdk">Download Objects</a>.</div>


<span id=".5YiX5Li-5a-56LGh"></span>
## Enumerated Objects

The following code demonstrates how to list up to 2,000 existing objects in a bucket. The initial request retrieves 1,000 objects. The isTruncated parameter is used to verify whether all objects have been listed. If additional objects remain, the listing continues based on the NextContinuationToken.

```cpp
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
  
    
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
  
    std::string bucketName = "examplebucket";

    
    InitializeClient();
  
    TosClientV2 client(region, accessKey, secretKey);

    ListObjectsType2Input input(bucketName);
    input.setMaxKeys(1000);
    auto output = client.listObjectsType2(input);
    if (!output.isSuccess()) {
       
        std::cout << "ListObjects failed." << output.error().String() << std::endl;
       
        CloseClient();
        return -1;
    }

    std::cout << "ListObjects success." << std::endl;
    for (const auto& object : output.result().getContents()) {
        std::cout << "object"<<
                ",name:" << object.getKey() <<
                ",size:" << object.getSize() <<
                ",lastmodify time:" << object.getStringFormatLastModified() <<
                ",storage class:" << object.getStringFormatStorageClass() << std::endl;
 
   
    if (output.result().isTruncated()){
        input.setContinuationToken(output.result().getNextContinuationToken());
        auto output1 = client.listObjectsType2(input);
        if (!output1.isSuccess()) {
          
            std::cout << "ListObjects failed." << output1.error().String() << std::endl;
          
            CloseClient();
            return -1;
        }

        std::cout << "ListObjects success." << std::endl;
        for (const auto& object : output1.result().getContents()) {
            std::cout << "object"<<
                    ",name:" << object.getKey() <<
                    ",size:" << object.getSize() <<
                    ",lastmodify time:" << object.getStringFormatLastModified() <<
                    ",storage class:" << object.getStringFormatStorageClass() << std::endl;
        }
    }
    
  
    CloseClient();
    return 0;
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more examples of object listing, please refer to <a href="https://docs.byteplus.com/docs/tos/List-objects-c-sdk">Object Listing</a>.</div>


<span id=".5Yig6Zmk5a-56LGh"></span>
## Delete Object

The following code demonstrates how to delete an object from a bucket.

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
    
    DeleteObjectInput input(bucketName, objectKey);
    auto output = client.deleteObject(input);
    if (!output.isSuccess()) {
       
        std::cout << "DeleteObject failed." << output.error().String() << std::endl;
        
        CloseClient();
        return -1;
    }

    std::cout << "DeleteObject success." << std::endl;
    std::cout << "DeleteObject request id:" << output.result().getRequestInfo().getRequestId() << std::endl;

    
    CloseClient();
    return 0;
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional example links on deleting objects, please see <a href="https://docs.byteplus.com/docs/tos/Delete-object-c-sdk">Deleting Objects</a>.</div>
