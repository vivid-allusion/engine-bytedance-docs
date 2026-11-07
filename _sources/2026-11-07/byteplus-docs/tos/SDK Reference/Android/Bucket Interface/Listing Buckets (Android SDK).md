---
title: "Listing Buckets (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-buckets-android-sdk"
---

A bucket is a container for storing objects. You can obtain the list of storage buckets (Bucket) by using listBuckets; this operation returns all buckets.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Before listing buckets, you must have the `tos:ListBuckets` permission. For detailed instructions, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).

* This interface returns all buckets across all regions for the current account.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to enumerate all buckets.

```java

import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.bucket.ListBucketsV2Input;
import com.volcengine.tos.model.bucket.ListBucketsV2Output;
import com.volcengine.tos.model.bucket.ListedBucket;

public class ListBucketExample extends AppCompatActivity {

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
                    ListBucketsV2Input input = new ListBucketsV2Input();
                    ListBucketsV2Output output = tos.listBuckets(input);
                    Log.i("listBuckets", "bucket owner is " + output.getOwner());
                    if (output.getBuckets() != null) {
                        Log.i("listBuckets", "you have listed " + output.getBuckets().size() + " buckets");
                        for (int i = 0; i < output.getBuckets().size(); i++){
                            ListedBucket bucket = output.getBuckets().get(i);
                            Log.i("listBuckets", "the No." + " bucket is " + bucket.toString());
                        }
                    } else {
                        Log.i("listBuckets", "there are no buckets in your account.");
                    }
                } catch (TosException e) {
                    Log.e("TosException", "listBuckets failed");
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

For documentation on the API for listing buckets, see [ListBuckets](https://docs.byteplus.com/docs/tos/reference-listbuckets).
