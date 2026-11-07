---
title: "Listing Multi-Version Objects (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-multi-version-objects-android-sdk"
---

The listObjectVersions API enables the enumeration of versioned object information within a bucket, returning up to 1,000 versioned objects per request.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter Description


|**Parameters** |**Description** |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |Character used for grouping object names. |
|keyMarker |The starting point for the enumeration of objects in this instance. |
|encodingType |Returns the key encoding type.<br><br>Default value: None |
|maxKeys |Maximum number of results to return. |
|versionIdMarker |Version number pagination identifier. |


<span id=".5YiX5Li-5omA5pyJ5aSa54mI5pys5a-56LGh"></span>
## List all multi\-version objects

The following code demonstrates how to list all multi\-version objects with pagination.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.ListObjectVersionsV2Input;
import com.volcengine.tos.model.object.ListObjectVersionsV2Output;
import com.volcengine.tos.model.object.ListedDeleteMarkerEntry;

public class ListObjectVersionsLoopExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        int maxKeys = 1000;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    boolean isTruncated = true;
                    String keyMarker = "";
                    String versionIDMarker = "";
                    int total = 0;
                    while (isTruncated) {
                        ListObjectVersionsV2Input input = new ListObjectVersionsV2Input()
                              
                                .setBucket(bucketName).setMaxKeys(maxKeys)
                                .setKeyMarker(keyMarker).setVersionIDMarker(versionIDMarker);
                        ListObjectVersionsV2Output output = tos.listObjectVersions(input);
                        Log.i("listObjectVersions", "listObjectVersions succeed, is truncated? " + output.isTruncated() +
                                "next key marker is " + output.getNextKeyMarker() + "next version id marker is" +
                                output.getNextVersionIDMarker());
                        if (output.getDeleteMarkers() != null) {
                            for (int i = 0; i < output.getDeleteMarkers().size(); i++) {
                                ListedDeleteMarkerEntry entry = output.getDeleteMarkers().get(i);
                                Log.i("listObjectVersions", "No." + (i+1+total) + " listed entry is " + entry);
                            }
                            total += output.getDeleteMarkers().size();
                        }
                        isTruncated = output.isTruncated();
                        keyMarker = output.getNextKeyMarker();
                        versionIDMarker = output.getVersionIDMarker();
                    }

                } catch (TosException e) {
                    Log.e("TosException", "listObjectVersions failed");
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

For API documentation on listing multi\-version objects, refer to [ListObjectsVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions).
