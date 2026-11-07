---
title: "Conditional Download (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Limited-download-android-sdk"
---

When downloading objects, you can specify one or more constraints. If the specified conditions are met, the download will proceed; otherwise, an error will be returned and the download will not occur.

<span id=".6ZmQ5a6a5p2h5Lu26K-05piO"></span>
## Specification of Constraints

The following are the specific conditions under which TOS support is provided.


|Parameters |Description |
|---|---|
|If\-Modified\-Since |If the specified time is earlier than the object's last modification time, the download proceeds normally; otherwise, a 304 error (Not Modified) is returned. |
|If\-Unmodified\-Since |If the specified time is equal to or later than the object's last modification time, the download proceeds normally; otherwise, a 412 error (Precondition Failed) is returned. |
|If\-Match |If the specified ETag matches the ETag of the object to be downloaded, the download proceeds normally; otherwise, a 412 error (Precondition Failed) is returned. |
|If\-None\-Match |If the specified ETag does not match the ETag of the object to be downloaded, the download proceeds normally; otherwise, a 304 error (Not Modified) is returned. |


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to set constraints for object download.

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
import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class GetObjectWithIfConditionExample extends AppCompatActivity {

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
                    
                    DateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
                    Date date = dateFormat.parse("2022-09-13 14:36:01");
                    ObjectMetaRequestOptions options = new ObjectMetaRequestOptions().setIfModifiedSince(date);
                    GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey).setOptions(options);
                    try(FileOutputStream fileOutputStream = new FileOutputStream(filePath);
                        GetObjectV2Output output = tos.getObject(input)) {
                        byte[] buffer = new byte[1024];
                        int length;
                        while ((length = output.getContent().read(buffer)) != -1) {
                            fileOutputStream.write(buffer, 0, length);
                        }
                        Log.i("getObject", "getObject succeed, object's metadata is " + output.getGetObjectBasicOutput());
                    } catch (IOException e) {
                        Log.e("IOException", "write data to file failed");
                        e.printStackTrace();
                    }
                } catch (TosException e) {
                    
                    if (e.getStatusCode() == 304) {
                        Log.e("TosException", "server return 304 not modified");
                    } else if (e.getStatusCode() == 412) {
                        
                        Log.e("TosException", "server return 412 precondition failed.");
                    } else if (e.getStatusCode() == 404) {
                       
                        Log.e("TosException", "the object you want to download is not found");
                    } else {
                        Log.e("TosException", "getObject failed");
                    }
                    e.printStackTrace();
                } catch (ParseException e) {
                    Log.e("ParseException", "getObject failed");
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

For the API documentation on downloading objects, see [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
