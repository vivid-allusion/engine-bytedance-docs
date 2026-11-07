---
title: "Deleting a Bucket (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-bucket-android-sdk"
---

You can use the deleteBucket interface to delete an empty bucket that does not contain any object data. For non\-empty buckets, you must first remove all objects and incomplete multipart upload tasks from the bucket before invoking this interface to perform the delete bucket operation.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Once a bucket is deleted, it cannot be restored. Please proceed with caution.

* Before deleting a bucket, you must have the `tos:DeleteBucket` permission. For specific operations, please refer to the [Permission Configuration Guide](https://docs.byteplus.com/docs/tos/docs-permission-configuration-guide).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before deleting a bucket, ensure that all data within the bucket has been deleted.


* If versioning is enabled for the bucket, please ensure that all current and previous version objects within the bucket have been deleted. For detailed procedures, please refer to [Delete Object](https://docs.byteplus.com/docs/tos/docs-versioning-related-operations#%E5%BD%BB%E5%BA%95%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6).

* If there are unmerged fragments in the bucket, please ensure that all fragment data is deleted. For specific instructions, see [Delete Fragment](https://docs.byteplus.com/docs/tos/docs-managing-parts#%E5%88%A0%E9%99%A4%E5%88%86%E7%89%87).

* If your bucket contains a large number of objects, you can configure bulk deletion by applying lifecycle rules. For detailed instructions, please refer to [Set Lifecycle Rules](https://docs.byteplus.com/docs/6349/75028).


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to delete empty buckets.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.bucket.DeleteBucketInput;
import com.volcengine.tos.model.bucket.DeleteBucketOutput;

public class DeleteBucketExample extends AppCompatActivity {

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
                    DeleteBucketInput input = new DeleteBucketInput().setBucket(bucketName);
                    DeleteBucketOutput output = tos.deleteBucket(input);
                    Log.i("deleteBucket", "deleteBucket succeed, " + output);
                } catch (TosException e) {
                    if (e.getStatusCode() == 404) {
                        Log.e("TosException", "deleteBucket failed, the bucket is not found.");
                    } else {
                        Log.e("TosException", "deleteBucket failed.");
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
## Relevant Documentation

For API documentation on deleting buckets, refer to [DeleteBucket](https://docs.byteplus.com/docs/tos/reference-deletebucket).
