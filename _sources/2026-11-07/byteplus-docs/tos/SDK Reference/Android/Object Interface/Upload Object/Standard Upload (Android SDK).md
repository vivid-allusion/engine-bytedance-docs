---
title: "Standard Upload (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Normal-upload-android-sdk"
---

The Android SDK supports uploading an object to the TOS server using either streaming or file\-based methods. This article describes how to upload your data using streaming upload and file upload methods.

<span id=".5LiK5Lyg6K-05piO"></span>
## Upload Instructions


* Streaming upload refers to the process of using stream\-based data sources, such as file streams, network streams, strings, or byte arrays, for TOS. These data sources are uniformly abstracted as the InputStream class for uploading.

* File Upload: Refers to using local files as the data source for TOS.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When uploading an object, if an object with the same name already exists in the bucket, the new object will overwrite the existing one. When multi\-versioning is enabled for a bucket, the original object is retained, and a new version number is generated to identify the newly uploaded object.</div>


<span id=".5LuO5YaF5a2Y5a2X56ym5rWBLeWtl-iKgua1geS4iuS8oA=="></span>
## Upload from memory character stream or byte stream

The SDK supports streaming uploads via the putObject interface.

The following code demonstrates how to upload a string or a byte array to TOS.

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

public class PutObjectByteExample extends AppCompatActivity {

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


<span id=".5LuO572R57uc5rWB5LiK5Lyg"></span>
## Upload via network stream

The following code demonstrates how to upload a network file to TOS as a network stream.

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

import java.io.IOException;
import java.io.InputStream;
import java.net.URL;

public class PutObjectFromUrlExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";
        
        String url = "https://www.byteplus.com/en/";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try(InputStream inputStream = new URL(url).openStream();){
                    PutObjectBasicInput basicInput = new PutObjectBasicInput().setBucket(bucketName).setKey(objectKey);
                    PutObjectInput putObjectInput = new PutObjectInput().setPutObjectBasicInput(basicInput).setContent(inputStream);
                    PutObjectOutput output = tos.putObject(putObjectInput);
                    Log.i("putObject", "putObject succeed, object's etag is " + output.getEtag());
                    Log.i("putObject", "putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException", "putObject failed");
                    e.printStackTrace();
                } catch (IOException e) {
                    Log.e("IOException", "putObject read file failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5LuO5pys5Zyw5paH5Lu25rWB5LiK5Lyg"></span>
## Upload from Local File Stream

The following code demonstrates how to upload a file stream (FileInputStream) to TOS.

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

import java.io.FileInputStream;
import java.io.IOException;

public class PutObjectFromFileInputStreamExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";
        String filePath = "your file's path to putObject";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try(FileInputStream inputStream = new FileInputStream(filePath)){
                    PutObjectBasicInput basicInput = new PutObjectBasicInput().setBucket(bucketName).setKey(objectKey);
                    PutObjectInput putObjectInput = new PutObjectInput().setPutObjectBasicInput(basicInput).setContent(inputStream);
                    PutObjectOutput output = tos.putObject(putObjectInput);
                    Log.i("putObject", "putObject succeed, object's etag is " + output.getEtag());
                    Log.i("putObject", "putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException", "putObject failed");
                    e.printStackTrace();
                } catch (IOException e) {
                    Log.e("IOException", "putObject read file failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5LuO5pys5Zyw5paH5Lu25LiK5Lyg"></span>
## Upload from local file

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.PutObjectBasicInput;
import com.volcengine.tos.model.object.PutObjectFromFileInput;
import com.volcengine.tos.model.object.PutObjectFromFileOutput;

public class PutObjectFromFileExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";
        String filePath = "your file's path to putObject";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    PutObjectBasicInput basicInput = new PutObjectBasicInput().setBucket(bucketName).setKey(objectKey);
                    PutObjectFromFileInput putObjectInput = new PutObjectFromFileInput().setPutObjectBasicInput(basicInput).setFilePath(filePath);
                    PutObjectFromFileOutput output = tos.putObjectFromFile(putObjectInput);
                    Log.i("putObjectFromFile", "putObject succeed, object's etag is " + output.getPutObjectOutput().getEtag());
                    Log.i("putObjectFromFile", "putObject succeed, object's crc64 is " + output.getPutObjectOutput().getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException", "putObjectFromFile failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5oyH5a6aLWFjbOOAgXN0b3JhZ2VjbGFzc-OAgeWvueixoeWFg-aVsOaNrg=="></span>
## Specify ACL, StorageClass, and object metadata

When performing streaming uploads or file uploads, the SDK supports setting metadata for the object to be uploaded through the PutObjectBasicInput class. The following code demonstrates how to set the metadata for an object to be uploaded.

```java

import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.comm.common.StorageClassType;
import com.volcengine.tos.model.object.ObjectMetaRequestOptions;
import com.volcengine.tos.model.object.PutObjectBasicInput;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.ByteArrayInputStream;
import java.util.HashMap;
import java.util.Map;

public class PutObjectWithMetaExample extends AppCompatActivity {

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
                    ObjectMetaRequestOptions options = new ObjectMetaRequestOptions();
                    
                    options.setAclType(ACLType.ACL_PRIVATE);
                    
                    options.setStorageClass(StorageClassType.STORAGE_CLASS_STANDARD);
                    
                    options.setContentType("application/json");
                    
                    options.setContentLanguage("en");
                    
                    options.setContentDisposition("attachment;filename=download.txt");
                 
                    options.setCacheControl("max-age=600");
                    
                    options.setContentMD5("yjtlyPoGKxvDj+QOPocqjg==");
                    
                    options.setServerSideEncryption("AES256");
                  
                    Map<String, String> custom = new HashMap<>();
                    custom.put("name", "volc_user");
                   
                    options.setCustomMetadata(custom);

                    PutObjectBasicInput basicInput = new PutObjectBasicInput().setBucket(bucketName).setKey(objectKey).setOptions(options);
                    PutObjectInput putObjectInput = new PutObjectInput().setPutObjectBasicInput(basicInput).setContent(stream);
                    PutObjectOutput output = tos.putObject(putObjectInput);
                    Log.i("putObject", "putObject succeed, object's etag is " + output.getEtag());
                    Log.i("putObject", "putObject succeed, object's crc64 is " + output.getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException", "putObject failed");
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

For API documentation on uploading objects, refer to [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject).
