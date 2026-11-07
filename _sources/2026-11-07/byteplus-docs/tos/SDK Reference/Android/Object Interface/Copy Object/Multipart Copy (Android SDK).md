---
title: "Multipart Copy (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Sharding-copy-android-sdk"
---

When an object exceeds 1 GiB in size, it is recommended to use uploadPartCopy for multipart copy operations. This article presents the steps and sample code for multipart copy.

<span id=".5YiG54mH5ou36LSd5q2l6aqk"></span>
## Steps


1. Initialize the multipart copy task using createMultipartUpload.

2. Perform multipart copy using uploadPartCopy.

3. Merge parts using completeMultipartUpload.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

The following code uses copyObject to copy the srcObjectKey object from the srcBucketName bucket to the bucketName bucket, and sets the object name to objectKey.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.CompleteMultipartUploadV2Input;
import com.volcengine.tos.model.object.CompleteMultipartUploadV2Output;
import com.volcengine.tos.model.object.CreateMultipartUploadInput;
import com.volcengine.tos.model.object.CreateMultipartUploadOutput;
import com.volcengine.tos.model.object.HeadObjectV2Input;
import com.volcengine.tos.model.object.HeadObjectV2Output;
import com.volcengine.tos.model.object.UploadPartCopyV2Input;
import com.volcengine.tos.model.object.UploadPartCopyV2Output;
import com.volcengine.tos.model.object.UploadedPartV2;

import java.util.ArrayList;
import java.util.List;

public class UploadPartCopyExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String srcBucketName = "your src bucket name";
        String srcObjectKey = "your src object key";
        String bucketName = "your bucket name";
        String objectKey = "your object key";
        long partSize = 10 * 1024 * 1024;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                  
                    HeadObjectV2Output headInfo = tos.headObject(new HeadObjectV2Input().setBucket(srcBucketName).setKey(srcObjectKey));
                    long contentLength = headInfo.getHeadObjectBasicOutput().getContentLength();

                    
                    CreateMultipartUploadInput create = new CreateMultipartUploadInput().setBucket(bucketName).setKey(objectKey);
                    CreateMultipartUploadOutput created = tos.createMultipartUpload(create);
                    String uploadID = created.getUploadID();

                  
                    List<UploadedPartV2> partList = new ArrayList<>();
                    
                    long rangeStart = 0, rangeEnd = 0;
                    int partNumber = 1;
                    while (rangeEnd < contentLength) {
                        
                        rangeEnd = Math.min(rangeStart + partSize - 1, contentLength);
                        UploadPartCopyV2Input input = new UploadPartCopyV2Input().setBucket(bucketName).setKey(objectKey)
                                .setUploadID(uploadID).setSourceBucket(srcBucketName).setSourceKey(srcObjectKey)
                                .setPartNumber(partNumber).setCopySourceRange(rangeStart, rangeEnd);
                        UploadPartCopyV2Output output = tos.uploadPartCopy(input);
                        Log.i("uploadPartCopy", "uploadPartCopy succeed, part's etag is " + output.getEtag());
                        Log.i("uploadPartCopy", "uploadPartCopy succeed, part's partNumber is " + output.getPartNumber());
                        partList.add(new UploadedPartV2().setEtag(output.getEtag()).setPartNumber(output.getPartNumber()));
                        rangeStart = rangeEnd + 1;
                        partNumber++;
                    }
                   
                    CompleteMultipartUploadV2Input complete = new CompleteMultipartUploadV2Input().setBucket(bucketName)
                            .setKey(objectKey).setUploadID(uploadID).setUploadedParts(partList);
                    CompleteMultipartUploadV2Output output = tos.completeMultipartUpload(complete);
                    Log.i("uploadPartCopy", "copyObject succeed, object's etag is " + output.getEtag());
                    Log.i("uploadPartCopy", "copyObject succeed, object's crc64 is " + output.getHashCrc64ecma());
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
## **Relevant documentation**


* For the API documentation on creating a multipart upload task, see [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For API documentation on multipart copy operations, refer to [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy).

* For API documentation on merging parts, refer to [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).
