---
title: "Supplementary Upload (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-android-sdk"
---

The SDK supports appending objects through the appendObject interface. Append write refers to appending content to the end of an already uploaded object. This interface can only be used with objects of the Appendable type. Objects created through direct upload or multipart upload are classified as Normal type, whereas objects uploaded via the appendObject interface are classified as Appendable type.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The object size limitations when using the appendObject interface are as follows:


* The total size of appended objects must not exceed 5 GiB.

* When an object is created using appendObject, performing a putObject operation on it will overwrite the object and change its type from Appendable to Normal. Conversely, objects uploaded via putObject do not support append write operations.

* Objects created by appendObject do not support copying.

* If your bucket has versioning enabled or suspended, or if the bucket type is infrequent access storage, you cannot use the appendObject interface to append objects.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to write objects to the target bucket using append mode.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.comm.common.StorageClassType;
import com.volcengine.tos.model.object.AppendObjectInput;
import com.volcengine.tos.model.object.AppendObjectOutput;
import com.volcengine.tos.model.object.ObjectMetaRequestOptions;

import java.io.ByteArrayInputStream;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class AppendObjectExample extends AppCompatActivity {

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
                  
                    byte[] data1 = new byte[128 * 1024];
                    Arrays.fill(data1, (byte) 'A');
                    ByteArrayInputStream stream = new ByteArrayInputStream(data1);
                   
                    ObjectMetaRequestOptions options = new ObjectMetaRequestOptions();
               
                    options.setAclType(ACLType.ACL_PRIVATE);
               
                    options.setStorageClass(StorageClassType.STORAGE_CLASS_STANDARD);
              
                    options.setContentType("application/json");
               
                    Map<String, String> custom = new HashMap<>();
                    custom.put("name", "volc_user");
                
                    options.setCustomMetadata(custom);

                   
                    long contentLength = data1.length;
                    long offset = 0;
                    AppendObjectInput input = new AppendObjectInput().setBucket(bucketName).setKey(objectKey)
                            .setContent(stream).setContentLength(contentLength).setOffset(offset).setOptions(options);
                    AppendObjectOutput output = tos.appendObject(input);
                    Log.i("appendObject", "appendObject first time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
                    Log.i("appendObject", "appendObject first time succeed, object's crc64 is " + output.getHashCrc64ecma());

                 
                    byte[] data2 = new byte[128 * 1024 + 1024];
                    Arrays.fill(data2, (byte) 'B');
              
                    contentLength = data2.length;
                    offset = data1.length;
                 
                    String preHashCrc64 = output.getHashCrc64ecma();
                    input = new AppendObjectInput().setBucket(bucketName).setKey(objectKey).setContent(new ByteArrayInputStream(data2))
                            .setOffset(offset).setContentLength(contentLength).setPreHashCrc64ecma(preHashCrc64);
                    output = tos.appendObject(input);
                    Log.i("appendObject", "appendObject second time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
                    Log.i("appendObject", "appendObject second time succeed, object's crc64 is " + output.getHashCrc64ecma());

                  
                    byte[] data3 = new byte[256 * 1024 + 1024];
                    Arrays.fill(data3, (byte) 'C');
                
                    contentLength = data3.length;
                    offset = data1.length + data2.length;
          
                    preHashCrc64 = output.getHashCrc64ecma();
                    input = new AppendObjectInput().setBucket(bucketName).setKey(objectKey).setContent(new ByteArrayInputStream(data3))
                            .setOffset(offset).setContentLength(contentLength).setPreHashCrc64ecma(preHashCrc64);
                    output = tos.appendObject(input);
                    Log.i("appendObject", "appendObject third time succeed, object's nextAppendOffset is " + output.getNextAppendOffset());
                    Log.i("appendObject", "appendObject third time succeed, object's crc64 is " + output.getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException", "appendObject failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Related Documents**

For API documentation regarding append upload, please refer to [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject).
