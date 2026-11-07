---
title: "Standard Copy (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-copy-android-sdk"
---

When the object is smaller than 1GiB, you can use standard copy. This article presents example code for basic copy operations.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code uses copyObject to copy the srcObjectKey object from the srcBucketName bucket to the bucketName bucket, and sets the object name to objectKey.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.CopyObjectV2Input;
import com.volcengine.tos.model.object.CopyObjectV2Output;

public class CopyObjectExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";

        String srcBucketName = "your src bucket name";
        String srcObjectKey = "your src object key";
        String bucketName = "your bucket name";
        String objectKey = "your object key";
        String securityToken = "your security token";
        
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    CopyObjectV2Input input = new CopyObjectV2Input().setBucket(bucketName).setKey(objectKey)
                            .setSrcBucket(srcBucketName).setSrcKey(srcObjectKey);
                    CopyObjectV2Output output = tos.copyObject(input);
                    Log.i("copyObject", "copyObject succeed, object's etag is " + output.getEtag());
                    Log.i("copyObject", "copyObject succeed, object's crc64 is " + output.getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException", "copyObject failed");
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

For API documentation on standard copy operations, refer to [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject).
