---
title: "Pre-Signature Mechanism (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Pre-signature-mechanism-android-sdk"
---

The SDK also supports generating signed URLs, which can be used to initiate HTTP requests directly or shared with third parties to enable access authorization.

<span id=".5pmu6YCa6aKE562-5ZCN"></span>
## Standard Pre\-Signature

The following example demonstrates how to download an object using a pre\-signed URL.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.comm.HttpMethod;

import java.time.Duration;

public class PreSignedUrlGetObjectExample extends AppCompatActivity {

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
                String signed = tos.preSignedURL(HttpMethod.GET, bucketName, objectKey, Duration.ofHours(1));
                Log.i("preSignedURL", "generated url is " + signed);
            }
        });

        tosThread.start();
    }
}
```
