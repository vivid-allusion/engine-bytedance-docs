---
title: "Managing the Functionality for Renaming Objects in Buckets (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-bucket-rename-object-functionality-c-sdk"
---

TOS supports the renaming of individual objects within a bucket. To use the object renaming feature, you must first enable the renaming function for the bucket.

<span id="27dbd1b8"></span>
## Configuring Bucket Renaming Rules

<span id="61045087"></span>
### **Precautions**


* The rename function cannot be enabled for multi\-version buckets.

* The `renameEnable` parameter can only be set to `True`.


<span id="8b3cdc8e"></span>
### **Sample Code**

The following code is used to enable the renaming feature for the bucket 'examplebucket'.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){
   
   
    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    
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
    
  
    CloseClient();
    return 0;
}
```


<span id="d4018531"></span>
## Retrieving bucket renaming rules

<span id="bd5d906f"></span>
### **Precautions**

To retrieve the bucket renaming rules, you must be the bucket owner by default.

<span id="0a5646f9"></span>
### **Sample Code**

The following code is used to retrieve the renaming rules for the bucket examplebucket.

```C++
#include "TosClientV2.h"
using namespace VolcengineTos;

int main(void){


    std::string region = "Your Region";
    std::string accessKey = std::getenv("TOS_ACCESS_KEY");
    std::string secretKey = std::getenv("TOS_SECRET_KEY");
    
    std::string bucketName = "examplebucket";
    
    
    InitializeClient();
  
    TosClientV2 client(region, accessKey, secretKey);
    
    GetBucketRenameInput input(bucketName);
    auto output = client.getBucketRename(input);
    if (!output.isSuccess()) {
       
        std::cout << "GetBucketRename failed." << output.error().String() << std::endl;
      
        CloseClient();
        return -1;
    }
    std::cout << "GetBucketRename success" << std::endl;
   
    CloseClient();
    return 0;
}
```


<span id="5e0b66fe"></span>
## Delete Bucket Renaming Rules

<span id="1ad5a520"></span>
### **Precautions**

Remove the bucket renaming rule; by default, you must be the bucket owner.

<span id="f4684f10"></span>
### **Sample Code**

The following code is used to delete the renaming rule for the bucket examplebucket.

```Java
import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.bucket.DeleteBucketRenameInput;
import com.volcengine.tos.model.bucket.DeleteBucketRenameOutput;

public class DeleteBucketRenameExample {
    public static void main(String[] args) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = System.getenv("TOS_ACCESS_KEY");
        String secretKey = System.getenv("TOS_SECRET_KEY");
        String bucketName = "bucket-example";

        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey);

        try{
            DeleteBucketRenameInput input = new DeleteBucketRenameInput().setBucket(bucketName);
            DeleteBucketRenameOutput output = tos.deleteBucketRename(input);
            System.out.println("deleteBucketRename succeed, " + output);
        } catch (TosClientException e) {
        
            System.out.println("deleteBucketRename failed");
            System.out.println("Message: " + e.getMessage());
            if (e.getCause() != null) {
                e.getCause().printStackTrace();
            }
        } catch (TosServerException e) {
          
            System.out.println("deleteBucketRename failed");
            System.out.println("StatusCode: " + e.getStatusCode());
            System.out.println("Code: " + e.getCode());
            System.out.println("Message: " + e.getMessage());
            System.out.println("RequestID: " + e.getRequestID());
        } catch (Throwable t) {
       
            System.out.println("deleteBucketPolicy failed");
            System.out.println("unexpected exception, message: " + t.getMessage());
        }
    }
}
```


<span id="3bd20754"></span>
## Relevant Documentation


* For detailed information about RenameObject, see [Using RenameObject](https://docs.byteplus.com/docs/tos/Use-renameobject).

* For details on the API for enabling bucket renaming rules, see [PutBucketRename](https://docs.byteplus.com/docs/tos/Putbucketrename).

* For API documentation on obtaining bucket renaming rules, refer to [GetBucketRename](https://docs.byteplus.com/docs/tos/Getbucketrename).

* For information about the API for disabling bucket renaming rules, please refer to [DeleteBucketRename](https://docs.byteplus.com/docs/tos/Deletebucketrename).
