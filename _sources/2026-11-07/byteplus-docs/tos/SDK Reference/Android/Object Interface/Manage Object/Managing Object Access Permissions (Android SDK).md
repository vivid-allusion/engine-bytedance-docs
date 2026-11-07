---
title: "Managing Object Access Permissions (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-access-to-objects-android-sdk"
---

This article describes how to obtain and configure access permissions for objects. Object access permissions take precedence over bucket access permissions. If no access permissions are set for an object, the bucket's access permissions will apply.

<span id=".5a-56LGh5p2D6ZmQ6K-05piO"></span>
## Description of Object Permissions


|**Access Permission Value** |**Description** |
|---|---|
|private |Private. The owner of the object possesses all permissions, while other users are not authorized to perform actions on the object. |
|public\-read |Public reading. The owner of an object possesses all permissions, while other users have only read permission for that object. |
|public\-read\-write |Public Read/Write. All users have read and write permissions for this object file. |
|authenticated\-read |The owner of the object possesses all permissions, while authenticated users are granted read access to the object. |
|bucket\-owner\-read |The object owner has full permissions, while the bucket owner has read permission for the object. |
|bucket\-owner\-full\-control |Both the bucket owner and the object owner have full operation permissions on the object. |


<span id=".6K6-572u5a-56LGh55qE6K6_6Zeu5p2D6ZmQ"></span>
## Configuring Object Access Permissions

The following code demonstrates how to set object access permissions using the putObjectAcl interface.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.model.object.PutObjectACLInput;
import com.volcengine.tos.model.object.PutObjectACLOutput;

public class PutObjectAclExample extends AppCompatActivity {

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
                    
                    PutObjectACLInput input = new PutObjectACLInput().setAcl(ACLType.ACL_PUBLIC_READ)
                            .setBucket(bucketName).setKey(objectKey);
                    PutObjectACLOutput output = tos.putObjectAcl(input);
                    Log.i("putObjectAcl", "putObjectAcl succeed, request info is " + output);
                } catch (TosException e) {
                    Log.e("TosException", "putObjectAcl failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".6I635Y-W5a-56LGh55qE6K6_6Zeu5p2D6ZmQ"></span>
## Obtaining access permissions for objects

The following code demonstrates how to obtain object access permissions using the getObjectAcl interface.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.GetObjectACLV2Input;
import com.volcengine.tos.model.object.GetObjectACLV2Output;

public class GetObjectAclExample extends AppCompatActivity {

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
                    GetObjectACLV2Input input = new GetObjectACLV2Input().setBucket(bucketName).setKey(objectKey);
                    GetObjectACLV2Output output = tos.getObjectAcl(input);
                    Log.i("getObjectAcl", "getObjectAcl succeed, full acl info is " + output);
                } catch (TosException e) {
                    Log.e("TosException", "getObjectAcl failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
### **Relevant Documentation**

For API documentation on obtaining read and write permissions for objects, refer to [GetObjectAcl](https://docs.byteplus.com/docs/tos/reference-getobjectacl).
