---
title: "Deleting Objects (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-object-android-sdk"
---

The deleteObject interface enables the deletion of a specified object. The deleteMultiObjects interface enables the deletion of a batch of objects specified in a given list.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description


|**Parameters** |**Description** |
|---|---|
|versionID |Version ID: If the bucket has versioning enabled, this parameter can be used to delete a specified version of an object. |


<span id=".5Yig6Zmk5a-56LGh"></span>
## Delete Object

The following code demonstrates how to delete an object.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.DeleteObjectInput;
import com.volcengine.tos.model.object.DeleteObjectOutput;

public class DeleteObjectExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";
        
        String versionID = "the specific version id";
        
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    DeleteObjectInput input = new DeleteObjectInput().setBucket(bucketName).setKey(objectKey);
                    DeleteObjectOutput output = tos.deleteObject(input);
                 
                    input.setVersionID(versionID);
                    Log.i("deleteObject", "succeed, " + output);
                } catch (TosException e) {
                    Log.e("TosException", "deleteObject failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5om56YeP5Yig6Zmk5a-56LGh"></span>
## Batch Delete Objects

The following code demonstrates how to perform batch deletion of objects.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.DeleteError;
import com.volcengine.tos.model.object.DeleteMultiObjectsV2Input;
import com.volcengine.tos.model.object.DeleteMultiObjectsV2Output;
import com.volcengine.tos.model.object.Deleted;
import com.volcengine.tos.model.object.ObjectTobeDeleted;

import java.util.ArrayList;
import java.util.List;

public class DeleteMultiObjectsExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";
     
        String versionID = "the specific version id";

        String objectKey1 = "your object key";
        
        String versionID1 = "the specific version id";

        String objectKey2 = "your object key";
        
        String versionID2 = "the specific version id";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    List<ObjectTobeDeleted> objs = new ArrayList<>();
                    objs.add(new ObjectTobeDeleted().setKey(objectKey).setVersionID(versionID));
                    objs.add(new ObjectTobeDeleted().setKey(objectKey1).setVersionID(versionID1));
                    objs.add(new ObjectTobeDeleted().setKey(objectKey2).setVersionID(versionID2));
                    DeleteMultiObjectsV2Input input = new DeleteMultiObjectsV2Input().setBucket(bucketName).setObjects(objs);
                    DeleteMultiObjectsV2Output output = tos.deleteMultiObjects(input);
                    Log.i("deleteMultiObjects", "deleteMultiObjects succeed, request info is " + output.getRequestInfo());
                    if (output.getDeleteds() != null) {
                        for (int i = 0; i < output.getDeleteds().size(); i++){
                            Deleted deleted = output.getDeleteds().get(i);
                            Log.i("deleteMultiObjects", "No." + i + " deleted object is " + deleted);
                        }
                    }
                    if (output.getErrors() != null) {
                        for (int i = 0; i < output.getErrors().size(); i++){
                            DeleteError error = output.getErrors().get(i);
                            Log.i("deleteMultiObjects", "No." + i + " delete error is " + error);
                        }
                    }
                } catch (TosException e) {
                    Log.e("TosException", "deleteMultiObjects failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## **Relevant Documentation**

For API documentation on deleting objects, refer to [DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject).
