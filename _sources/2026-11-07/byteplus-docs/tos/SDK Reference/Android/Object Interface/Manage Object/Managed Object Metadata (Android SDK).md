---
title: "Managed Object Metadata (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-metadata-android-sdk"
---

Object metadata refers to the description of an object's attributes, comprising both HTTP standard attributes (HTTP Header) and user\-defined metadata (User Meta).

<span id=".6K6-572u5a-56LGh5YWD5pWw5o2u"></span>
## Set Object Metadata

The following code demonstrates how to set an object's `Content-Type` via the setObjectMeta interface, as well as configure custom metadata to identify the object's purpose, attributes, etc.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.comm.common.StorageClassType;
import com.volcengine.tos.model.object.ObjectMetaRequestOptions;
import com.volcengine.tos.model.object.SetObjectMetaInput;
import com.volcengine.tos.model.object.SetObjectMetaOutput;

import java.io.ByteArrayInputStream;
import java.util.HashMap;
import java.util.Map;

public class SetObjectMetaExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    String data = "1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'";
                    ByteArrayInputStream stream = new ByteArrayInputStream(data.getBytes());
                    ObjectMetaRequestOptions options = new ObjectMetaRequestOptions();
                    
                    options.setAclType(ACLType.ACL_PRIVATE);
                    
                    options.setStorageClass(StorageClassType.STORAGE_CLASS_STANDARD);
                    
                    options.setContentType("application/json");
                
                    options.setContentLanguage("en");
                 
                    options.setContentDisposition("attachment;filename=download.txt");
                    
                    options.setCacheControl("max-age=600");
                
                    options.setContentMD5("yjtlyPoGKxvDj+QOPocqjg==");
                    
                    options.setServerSideEncryption("AES256");
                   
                    Map<String, String> custom = new HashMap<>();
                    custom.put("name", "volc_user");
                    
                    options.setCustomMetadata(custom);

                    SetObjectMetaInput input = new SetObjectMetaInput().setBucket(bucketName).setKey(objectKey)
                            .setOptions(options);
                    SetObjectMetaOutput output = tos.setObjectMeta(input);
                    Log.i("setObjectMeta", "setObjectMeta succeed, request info is " + output);
                } catch (TosException e) {
                    Log.e("TosException", "setObjectMeta failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".6I635Y-W5a-56LGh5YWD5pWw5o2u"></span>
## Retrieve Object Metadata

The headObject interface enables retrieval of object information, verification of object existence, and access to object metadata. The following code demonstrates how to retrieve the metadata of an object.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.HeadObjectV2Input;
import com.volcengine.tos.model.object.HeadObjectV2Output;

public class HeadObjectExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    HeadObjectV2Input input = new HeadObjectV2Input().setBucket(bucketName).setKey(objectKey);
                    HeadObjectV2Output output = tos.headObject(input);
                    Log.i("headObject", "headObject succeed, object's metadata is " + output.getHeadObjectBasicOutput());
                } catch (TosException e) {
                    if (e.getStatusCode() == 404) {
                        
                        Log.e("TosException", "the object you want to head is not found");
                    } else {
                        Log.e("TosException", "headObject failed");
                    }
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documents**

For API documentation on setting object metadata, refer to [SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta).
