---
title: "List Objects (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-android-sdk"
---

The listObjects interface enables the enumeration of object information within a bucket based on a specified prefix, returning up to 1,000 objects per request. By default, the results return the owner information of the bucket.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameters


|**Parameter** |**Description** |
|---|---|
|prefix |The prefix of the current query results. |
|delimiter |The character used for grouping object names; the default value is `/`. |
|marker |The starting point of the subjects listed here. |
|encodingType |Returns the key encoding type. |
|maxKeys |Maximum return count, with an upper limit of 1,000; that is, up to 1,000 objects can be returned in a single listing operation. |


<span id=".5YiX5Li-5omA5pyJ5a-56LGh"></span>
## List all objects

The following code demonstrates how to list all objects in a specified bucket.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.ListObjectsV2Input;
import com.volcengine.tos.model.object.ListObjectsV2Output;
import com.volcengine.tos.model.object.ListedObjectV2;

public class ListObjectLoopExample extends AppCompatActivity {

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
                    String marker = "";
                    int total = 0;
                    while (isTruncated) {
                        ListObjectsV2Input input = new ListObjectsV2Input()
                                
                                .setBucket(bucketName).setMaxKeys(maxKeys).setMarker(marker);
                        ListObjectsV2Output output = tos.listObjects(input);
                        Log.i("listObjects", "listObjects succeed, is truncated? " + output.isTruncated() + "next marker is " + output.getNextMarker());
                        if (output.getContents() != null) {
                            for (int i = 0; i < output.getContents().size(); i++) {
                                ListedObjectV2 object = output.getContents().get(i);
                                Log.i("listObjects", "No." + (i+1+total) + " listed object is " + object);
                            }
                            total += output.getContents().size();
                        }
                        isTruncated = output.isTruncated();
                        marker = output.getNextMarker();
                    }
                } catch (TosException e) {
                    Log.e("TosException", "listObjects failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5YiX5Li-5oyH5a6a5YmN57yA55qE5omA5pyJ5a-56LGh"></span>
## List all objects with the specified prefix

The following code demonstrates how to list all objects with a specified prefix.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.ListObjectsV2Input;
import com.volcengine.tos.model.object.ListObjectsV2Output;
import com.volcengine.tos.model.object.ListedObjectV2;

public class ListObjectsByPrefixExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        int maxKeys = 1000;
        String prefix = "the specific prefix";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    boolean isTruncated = true;
                    String marker = "";
                    int total = 0;
                    while (isTruncated) {
                        ListObjectsV2Input input = new ListObjectsV2Input()
                               
                                .setBucket(bucketName).setMaxKeys(maxKeys).setMarker(marker).setPrefix(prefix);
                        ListObjectsV2Output output = tos.listObjects(input);
                        Log.i("listObjects", "listObjects succeed, is truncated? " + output.isTruncated() + "next marker is " + output.getNextMarker());
                        if (output.getContents() != null) {
                            for (int i = 0; i < output.getContents().size(); i++) {
                                ListedObjectV2 object = output.getContents().get(i);
                                Log.i("listObjects", "No." + (i+1+total) + " listed object is " + object);
                            }
                            total += output.getContents().size();
                        }
                        isTruncated = output.isTruncated();
                        marker = output.getNextMarker();
                    }
                } catch (TosException e) {
                    Log.e("TosException", "listObjects failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5YiX5Li-5oyH5a6a5L2N572u5ZCO55qE5a-56LGh"></span>
## **List objects following the specified position**

Setting the `marker` parameter specifies the starting position for listing. The TOS service will return all objects whose string values follow `marker` in lexicographical order.

The following code demonstrates how to list objects after a specified starting position.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.ListObjectsV2Input;
import com.volcengine.tos.model.object.ListObjectsV2Output;
import com.volcengine.tos.model.object.ListedObjectV2;

public class ListObjectsByMarkerExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        int maxKeys = 1000;
        
        String initMarker = "the specific marker";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    boolean isTruncated = true;
                    String marker = initMarker;
                    int total = 0;
                    while (isTruncated) {
                        ListObjectsV2Input input = new ListObjectsV2Input()
                             
                                .setBucket(bucketName).setMaxKeys(maxKeys).setMarker(marker);
                        ListObjectsV2Output output = tos.listObjects(input);
                        Log.i("listObjects", "listObjects succeed, is truncated? " + output.isTruncated() + "next marker is " + output.getNextMarker());
                        if (output.getContents() != null) {
                            for (int i = 0; i < output.getContents().size(); i++) {
                                ListedObjectV2 object = output.getContents().get(i);
                                Log.i("listObjects", "No." + (i+1+total) + " listed object is " + object);
                            }
                            total += output.getContents().size();
                        }
                        isTruncated = output.isTruncated();
                        marker = output.getNextMarker();
                    }
                } catch (TosException e) {
                    Log.e("TosException", "listObjects failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5YiX5Li-5oyH5a6a55uu5b2V5LiL55qE5paH5Lu25ZKM5a2Q55uu5b2V"></span>
## **List objects and subdirectories in the specified directory**

TOS provides file semantics only and does not support folder semantics. To simulate directory functionality, create a zero\-byte object that ends with a forward slash (`/`).

The functionality of a directory can be simulated using the `delimiter` and `prefix` parameters:


* First, set the `delimiter` to `/`. By simultaneously setting `prefix` to an empty value, objects and subdirectory information in the root directory can be returned.

* When setting the `delimiter` to `/`. Simultaneously, when `prefix` is set as a subdirectory, objects and subdirectories within that subdirectory can be returned.


The following code is used to list objects and subdirectories within the specified directory.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.ListObjectsV2Input;
import com.volcengine.tos.model.object.ListObjectsV2Output;
import com.volcengine.tos.model.object.ListedObjectV2;

public class ListObjectsByDelimiterExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        int maxKeys = 1000;
        String prefix = "the specific prefix";
        String delimiter = "/";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    boolean isTruncated = true;
                    String marker = "";
                    int total = 0;
                    while (isTruncated) {
                        ListObjectsV2Input input = new ListObjectsV2Input()
                           
                                .setBucket(bucketName).setMaxKeys(maxKeys).setMarker(marker).setPrefix(prefix).setDelimiter(delimiter);
                        ListObjectsV2Output output = tos.listObjects(input);
                        Log.i("listObjects", "listObjects succeed, is truncated? " + output.isTruncated() + "next marker is " + output.getNextMarker());
                        if (output.getContents() != null) {
                            for (int i = 0; i < output.getContents().size(); i++) {
                                ListedObjectV2 object = output.getContents().get(i);
                                Log.i("listObjects", "No." + (i+1+total) + " listed object is " + object);
                            }
                            total += output.getContents().size();
                        }
                        isTruncated = output.isTruncated();
                        marker = output.getNextMarker();
                    }
                } catch (TosException e) {
                    Log.e("TosException", "listObjects failed");
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

For API documentation on listing objects, refer to [ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects).
