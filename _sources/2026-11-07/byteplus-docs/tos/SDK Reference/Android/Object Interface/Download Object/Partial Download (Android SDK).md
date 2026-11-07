---
title: "Partial Download (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Scope-download-android-sdk"
---

Range download refers to downloading only a portion of object data. You can specify the range of data to be downloaded by setting the range parameter in the getObject API.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to download a portion of an object.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;
import com.volcengine.tos.model.object.ObjectMetaRequestOptions;

import java.io.FileOutputStream;
import java.io.IOException;

public class GetObjectRangeExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
       
        String objectKey = "your object key";
        String filePath = "your file path";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                   
                    long rangeStart = 0;
                    long rangeEnd = 1023;
                    ObjectMetaRequestOptions options = new ObjectMetaRequestOptions().setRange(rangeStart, rangeEnd);
                    GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey).setOptions(options);
                    try(FileOutputStream fileOutputStream = new FileOutputStream(filePath);
                        GetObjectV2Output output = tos.getObject(input)) {
                        byte[] buffer = new byte[1024];
                        int length;
                        while ((length = output.getContent().read(buffer)) != -1) {
                            fileOutputStream.write(buffer, 0, length);
                        }
                        Log.i("getObject","getObject succeed, object's metadata is " + output.getGetObjectBasicOutput());
                    } catch (IOException e) {
                        Log.e("IOException", "write data to file failed");
                        e.printStackTrace();
                    }
                } catch (TosException e) {
                    if (e.getStatusCode() == 404) {
                        
                        Log.e("TosException", "the object you want to download is not found");
                    } else {
                        Log.e("TosException", "getObject failed");
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

For API documentation on downloading objects, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
