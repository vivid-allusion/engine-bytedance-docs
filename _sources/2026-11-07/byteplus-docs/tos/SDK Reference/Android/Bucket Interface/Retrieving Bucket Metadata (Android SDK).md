---
title: "Retrieving Bucket Metadata (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-metadata-android-sdk"
---

A storage bucket is a container of objects. You can use the headBucket interface to determine whether a bucket exists and to retrieve its metadata.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before you can retrieve bucket metadata, you must have the `tos:HeadBucket` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* If the bucket does not exist, this interface will return a 404 error. This interface is also commonly used to verify whether a bucket exists.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to retrieve bucket information.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.bucket.HeadBucketV2Input;
import com.volcengine.tos.model.bucket.HeadBucketV2Output;

public class HeadBucketExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    HeadBucketV2Input input = new HeadBucketV2Input().setBucket(bucketName);
                    HeadBucketV2Output output = tos.headBucket(input);
                    Log.i("headBucket", "bucket's region is " + output.getRegion());
                    Log.i("headBucket", "bucket's storage class is " + output.getStorageClass());
                } catch (TosException e) {
                    if (e.getStatusCode() == 404) {
                        Log.e("TosException", "headBucket failed, the bucket is not found.");
                    } else {
                        Log.e("TosException", "headBucket failed.");
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
## **Relevant Documentation**

For API documentation on retrieving bucket metadata, refer to [HeadBucket](https://docs.byteplus.com/docs/tos/reference-headbucket).
