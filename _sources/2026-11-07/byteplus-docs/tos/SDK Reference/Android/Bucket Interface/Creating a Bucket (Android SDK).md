---
title: "Creating a Bucket (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-bucket-android-sdk"
---

A Bucket is the globally unique namespace in TOS, functioning as a data container used to store Object data. The name of a newly created bucket must be unique within TOS.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The [naming conventions](https://docs.byteplus.com/docs/tos/docs-common-concepts) for storage buckets are as follows:

   * Only lowercase letters a–z, digits, and hyphens (\-) are permitted.

   * The first and last character must be a digit or a letter.

   * The length must be between 3 and 63 characters.

* When accessing TOS from other BytePlus products within the same region, it is recommended to use the intranet endpoint. For more information about regions and Endpoints, see [Regions and Access Domains](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

* Before creating a storage bucket, you must ensure that your account has the `tos:CreateBucket` permission. You can grant the corresponding permissions through IAM policies. For detailed steps, see [ IAM policies](https://docs.byteplus.com/docs/tos/docs-overview_6).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to create a new bucket.

```java

import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.comm.common.StorageClassType;
import com.volcengine.tos.model.bucket.CreateBucketV2Input;
import com.volcengine.tos.model.bucket.CreateBucketV2Output;

public class CreateBucketFullExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
     
        ACLType aclType = ACLType.ACL_PRIVATE;
      
        StorageClassType storageClassType = StorageClassType.STORAGE_CLASS_STANDARD;
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    CreateBucketV2Input input = new CreateBucketV2Input().setBucket(bucketName)
                            .setAcl(aclType).setStorageClass(storageClassType);
                    CreateBucketV2Output output = tos.createBucket(input);
                    Log.i("createBucket", output.getLocation());
                } catch (TosException e) {
                    Log.e("TosException", "createBucket failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For API documentation on creating buckets, refer to [CreateBucket](https://docs.byteplus.com/docs/tos/reference-createbucket).
