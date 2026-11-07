---
title: "Quick Start (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start-android-sdk"
---

This document describes how to perform common operations using the TOS Android SDK, such as creating buckets and uploading, downloading, or deleting objects, etc.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Install SDK](https://docs.byteplus.com/docs/tos/Install-the-android-sdk)

2. [Initialize Client](https://docs.byteplus.com/docs/tos/Initialize-client-side-android-sdk)


<span id=".5a6i5oi356uv6YCa55So56S65L6L"></span>
## General Client\-Side Examples

The Android SDK currently provides only synchronous request interfaces. To initiate requests properly within an Android application, asynchronous encapsulation is required. The following code demonstrates a general example of asynchronous SDK usage.

```java
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.util.Log;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosClientException;
import com.volcengine.tos.TosServerException;
import com.volcengine.tos.model.object.PutObjectBasicInput;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.ByteArrayInputStream;

public class DisplayMessageActivity extends AppCompatActivity {
    private TOSV2 tos;
    String endpoint = "your endpoint";
    String region = "your region";
    String accessKey = "your access key";
    String secretKey = "your secret key";
    String securityToken = "your security token";

    String bucketName = "your bucket name";
    String objectKey = "your object key";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try  {
                    String data = "1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'";
                    ByteArrayInputStream stream = new ByteArrayInputStream(data.getBytes());
                    PutObjectBasicInput basicInput = new PutObjectBasicInput().setBucket(bucketName).setKey(objectKey);
                    PutObjectInput putObjectInput = new PutObjectInput().setPutObjectBasicInput(basicInput).setContent(stream);
                    PutObjectOutput output = tos.putObject(putObjectInput);
                    Log.i("putObject", "object's etag is " + output.getEtag());
                    Log.i("putObject", "object's crc64 is " + output.getHashCrc64ecma());
                } catch (TosServerException e) {
                    Log.e("TosServerException", e.toString());
                } catch (TosClientException e) {
                    Log.e("TosClientException", e.toString());
                } catch (Throwable t) {
                    t.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5Yib5bu65qG2"></span>
## Create Bucket

A bucket is the globally unique namespace in TOS, functioning as a data container for storing object data. The following code demonstrates how to create a new bucket.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.bucket.CreateBucketV2Input;
import com.volcengine.tos.model.bucket.CreateBucketV2Output;

public class CreateBucketExample extends AppCompatActivity {

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
                    CreateBucketV2Input input = new CreateBucketV2Input().setBucket(bucketName);
                    CreateBucketV2Output output = tos.createBucket(input);
                    Log.i("bucket created: ", output.getLocation());
                } catch (TosException e) {
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5LiK5Lyg5a-56LGh"></span>
## Upload Object

After successfully creating a bucket, you can upload objects to it. The following section demonstrates how to upload an object to the newly created bucket.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.PutObjectBasicInput;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.ByteArrayInputStream;

public class PutObjectBasicExample extends AppCompatActivity {

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
                try{
                    String data = "1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'1234567890abcdefghijklmnopqrstuvwxyz~!@#$%^&*()_+<>?,./   :'";
                    ByteArrayInputStream stream = new ByteArrayInputStream(data.getBytes());
                    PutObjectBasicInput basicInput = new PutObjectBasicInput().setBucket(bucketName).setKey(objectKey);
                    PutObjectInput putObjectInput = new PutObjectInput().setPutObjectBasicInput(basicInput).setContent(stream);
                    PutObjectOutput output = tos.putObject(putObjectInput);
                    Log.i("putObject", "succeed, object's etag is " + output.getEtag());
                    Log.i("putObject", "succeed, object's crc64 is " + output.getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("putObject",  "failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you wish to upload an object to a specific folder (a logical concept in object storage), you can add to the object name a prefix of<code>/</code>A prefix at the end of the object name supports multi\-level folders. For example, the object name <code>folder1/folder2/objectName</code> means that objectName will be uploaded to folder2, which is inside folder1.</div>


* <div data-tips="true" data-tips-type="tip">When uploading an object to a folder, the folder exists only as a logical concept within object storage; consequently, no actual folder is created on the object storage server.</div>


* <div data-tips="true" data-tips-type="tip">When downloading an object, you must use the full path with the appropriate prefix. For example, the object name to be provided during download should also be <code>folder1/folder2/objectName</code>.</div>


* <div data-tips="true" data-tips-type="tip">For additional examples of uploading objects, refer to <a href="https://docs.byteplus.com/docs/tos/Normal-upload-android-sdk">Standard Upload</a>.</div>



<span id=".5LiL6L295a-56LGh"></span>
## Download Object

The following demonstrates how to download an existing object from a bucket.

```java

import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.FileOutputStream;
import java.io.IOException;

public class GetObjectBasicExample extends AppCompatActivity {

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
                    GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey);
                   
                    try(FileOutputStream fileOutputStream = new FileOutputStream(filePath);
                        GetObjectV2Output output = tos.getObject(input)) {
                        byte[] buffer = new byte[1024];
                        int length;
                        while ((length = output.getContent().read(buffer)) != -1) {
                            fileOutputStream.write(buffer, 0, length);
                        }
                        Log.i("getObject", "succeed, object's metadata is " + output.getGetObjectBasicOutput());
                    } catch (IOException e) {
                        Log.e("IOException", "write data to file failed");
                        e.printStackTrace();
                    }
                } catch (TosException e) {
                    if (e.getStatusCode() == 404) {
                       
                        Log.e("TosException", "the object you want to download is not found");
                        e.printStackTrace();
                    } else {
                        Log.e("TosException", "getObject failed");
                        e.printStackTrace();
                    }
                }
            }
        });

        tosThread.start();
    }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more examples of download objects, see <a href="https://docs.byteplus.com/docs/tos/Normal-download-android-sdk">Standard Download</a>.</div>


<span id=".5YiX5Li-5a-56LGh"></span>
## Enumerated Objects

The following demonstrates how to list uploaded objects from a bucket.

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

public class ListObjectBasicExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        int maxKeys = 10;

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    ListObjectsV2Input input = new ListObjectsV2Input()
                           
                            .setBucket(bucketName).setMaxKeys(maxKeys);
                    ListObjectsV2Output output = tos.listObjects(input);
                    Log.i("listObjects", "listObjects succeed, is truncated? " + output.isTruncated() + "next marker is " + output.getNextMarker());
                    if (output.getContents() != null) {
                        for (int i = 0; i < output.getContents().size(); i++) {
                            ListedObjectV2 object = output.getContents().get(i);
                            Log.i("listObjects", "No." + (i+1) + " listed object is " + object);
                        }
                    }
                    // list by next marker
                    input = new ListObjectsV2Input().setBucket(bucketName).setMaxKeys(maxKeys).setMarker(output.getNextMarker());
                    output = tos.listObjects(input);
                    Log.i("listObjects", "listObjects succeed, is truncated? " + output.isTruncated() + "next marker is " + output.getNextMarker());
                    if (output.getContents() != null) {
                        for (int i = 0; i < output.getContents().size(); i++) {
                            ListedObjectV2 object = output.getContents().get(i);
                            Log.i("listObjects", "No." + (i+1) + " listed object is " + object);
                        }
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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more examples of objects to be enumerated, see <a href="https://docs.byteplus.com/docs/tos/List-objects-android-sdk">Enumerating Objects</a>.</div>


<span id=".5Yig6Zmk5a-56LGh"></span>
## Delete Object

The following demonstrates how to delete an existing object from a bucket.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.DeleteObjectInput;
import com.volcengine.tos.model.object.DeleteObjectOutput;

public class DeleteObjectBasicExample extends AppCompatActivity {

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
                try{
                    DeleteObjectInput input = new DeleteObjectInput().setBucket(bucketName).setKey(objectKey);
                    DeleteObjectOutput output = tos.deleteObject(input);
                    Log.i("deleteObject", "succeed, " + output);
                } catch (TosException e) {
                    Log.e("TosException", "deleteObject failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For additional examples of deleting objects, see <a href="https://docs.byteplus.com/docs/tos/Delete-object-android-sdk">Deleting Objects</a>.</div>
