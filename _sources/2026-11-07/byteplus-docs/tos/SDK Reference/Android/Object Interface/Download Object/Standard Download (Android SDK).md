---
title: "Standard Download (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-download-android-sdk"
---

Standard download refers to downloading the complete object from a specified bucket using the SDK's getObject method. Before using this interface, please ensure that you have read access to this object.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to download an object.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

public class GetObjectInStringExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";

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
                    GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey);
                    
                    try(GetObjectV2Output output = tos.getObject(input);
                        BufferedReader reader = new BufferedReader(new InputStreamReader(output.getContent()))) {
                        Log.i("getObject", "begin to read content in object.");
                        while (true) {
                            String line = reader.readLine();
                            if (line == null) {
                                break;
                            }
                            Log.i("getObject", line);
                        }
                        Log.i("getObject", "getObject succeed, object's metadata is " + output.getGetObjectBasicOutput());
                    } catch (IOException e) {
                        Log.e("IOException", "read data in object failed");
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
## **Relevant Documents**

For API documentation on downloading objects, refer to [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject).
