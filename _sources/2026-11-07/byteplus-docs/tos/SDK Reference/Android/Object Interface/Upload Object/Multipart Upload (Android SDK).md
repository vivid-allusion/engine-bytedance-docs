---
title: "Multipart Upload (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-upload-android-sdk"
---

For larger objects, the object data can be divided into multiple parts for separate upload, and all uploaded parts are finally merged into a single object.

<span id=".5YiG54mH5LiK5Lyg5q2l6aqk"></span>
## Chunked Upload Procedure

Multipart upload consists of three fundamental steps:


1. Initialize the multipart upload task using createMultipartUpload.

   Before uploading multipart data, you must first initialize the process and obtain an uploadID for the multipart upload task using the createMultipartUpload API. The uploadID parameter is required for subsequent operations, including uploading parts, merging parts, canceling the multipart upload, and listing uploaded parts. Initializing a multipart upload task does not affect existing objects with the same name.

2. Perform multipart upload using uploadPart.

   Use this interface to upload chunk data. You must specify the uploadID obtained through createMultipartUpload, as well as the part number, which must be within the range [1, 10000]. For the same object and the same fragment task, multiple fragments can be uploaded concurrently, and the upload order does not affect the final fragment merge operation. Except for the last fragment, the size of each fragment must be at least 4 MiB.

   The SDK supports direct multipart upload via uploadPart, as well as file\-based multipart upload via uploadPartFromFile.

3. All parts are merged into a single object using completeMultipartUpload.

   This interface is used to merge data fragments that have already been uploaded. When invoking this interface, you must provide a valid list of parts (including `partNumber` and `etag`). After the TOS server receives the request, it will merge the parts into a single object based on the provided list.


<span id=".56S65L6L5Luj56CB"></span>
### Sample Code

The following code demonstrates how to perform a multipart upload of an object using the multipart interface.

```java

import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.common.ACLType;
import com.volcengine.tos.comm.common.StorageClassType;
import com.volcengine.tos.comm.io.TosRepeatableBoundedFileInputStream;
import com.volcengine.tos.model.object.CompleteMultipartUploadV2Input;
import com.volcengine.tos.model.object.CompleteMultipartUploadV2Output;
import com.volcengine.tos.model.object.CreateMultipartUploadInput;
import com.volcengine.tos.model.object.CreateMultipartUploadOutput;
import com.volcengine.tos.model.object.ObjectMetaRequestOptions;
import com.volcengine.tos.model.object.UploadPartBasicInput;
import com.volcengine.tos.model.object.UploadPartFromFileInput;
import com.volcengine.tos.model.object.UploadPartFromFileOutput;
import com.volcengine.tos.model.object.UploadPartV2Input;
import com.volcengine.tos.model.object.UploadPartV2Output;
import com.volcengine.tos.model.object.UploadedPartV2;

import java.io.ByteArrayInputStream;
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class MultipartUploadExample extends AppCompatActivity {
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
                String uploadID = null;
               
                try{
                    CreateMultipartUploadInput create = new CreateMultipartUploadInput().setBucket(bucketName).setKey(objectKey);
                   
                    ObjectMetaRequestOptions options = new ObjectMetaRequestOptions();
               
                    options.setAclType(ACLType.ACL_PRIVATE);
                   
                    options.setStorageClass(StorageClassType.STORAGE_CLASS_STANDARD);
           
                    options.setContentType("text/plain");
              
                    options.setContentLanguage("en-US");
                   
                    options.setContentDisposition("attachment;filename=123.txt");
                  
                    options.setCacheControl("no-cache, no-store, must-revalidate");
                  
                    options.setServerSideEncryption("AES256");
                    
                    Map<String, String> custom = new HashMap<>();
                    custom.put("name", "volc_user");
            
                    options.setCustomMetadata(custom);
                    create.setOptions(options);

                    CreateMultipartUploadOutput createOutput = tos.createMultipartUpload(create);
                    Log.i("createMultipartUpload", "createMultipartUpload succeed, uploadID is " + createOutput.getUploadID());

                    uploadID = createOutput.getUploadID();
                } catch (TosException e) {
                    Log.e("TosException",  "createMultipartUpload failed");
                    e.printStackTrace();
                }

         
                long partSize = 5 * 1024 * 1024;
       
                List<UploadedPartV2> uploadedParts = new ArrayList<>(5);
          。
                String filePath = "your data file path";
                for (int i = 1; i <= 3; ++i) {
                    try{
                        FileInputStream content = new FileInputStream(filePath);
                        InputStream wrappedContent = new TosRepeatableBoundedFileInputStream(content, partSize);
                        
                        long skip = (i-1) * partSize;
                        content.skip(skip);
                        UploadPartBasicInput basicInput = new UploadPartBasicInput().setBucket(bucketName)
                                .setKey(objectKey).setUploadID(uploadID).setPartNumber(i);
                        UploadPartV2Input input = new UploadPartV2Input().setUploadPartBasicInput(basicInput)
                                .setContentLength(partSize).setContent(wrappedContent);
                        UploadPartV2Output output = tos.uploadPart(input);
                  
                        uploadedParts.add(new UploadedPartV2().setPartNumber(i).setEtag(output.getEtag()));
                        Log.i("uploadPart", "uploadPart succeed, partNumber is " + output.getPartNumber() + ", etag is " +
                                output.getEtag() + ", crc64 value is " + output.getHashCrc64ecma());
                    }catch (IOException | TosException e) {
                        Log.e("TosException", "uploadPart failed");
                        e.printStackTrace();
                    }
                }

     
                try{
                    UploadPartBasicInput basicInput = new UploadPartBasicInput().setBucket(bucketName)
                            .setKey(objectKey).setUploadID(uploadID).setPartNumber(4);
         

                    long offset = 3 * partSize;
                    UploadPartFromFileInput input = new UploadPartFromFileInput().setUploadPartBasicInput(basicInput)
                            .setFilePath(filePath).setPartSize(partSize).setOffset(offset);
                    UploadPartFromFileOutput output = tos.uploadPartFromFile(input);
          
                    uploadedParts.add(new UploadedPartV2().setPartNumber(4).setEtag(output.getUploadPartV2Output().getEtag()));
                    Log.i("createMultipartUpload", "uploadPart succeed, partNumber is " + output.getUploadPartV2Output().getPartNumber() +
                            ", etag is " + output.getUploadPartV2Output().getEtag() + ", crc64 value is " + output.getUploadPartV2Output().getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException", "uploadPart failed");
                    e.printStackTrace();
                }

              
                try{
                    UploadPartBasicInput basicInput = new UploadPartBasicInput().setBucket(bucketName)
                            .setKey(objectKey).setUploadID(uploadID).setPartNumber(5);
             
        。
                    byte[] data = new byte[(int)partSize];
                    InputStream content = new ByteArrayInputStream(data);
                    UploadPartV2Input input = new UploadPartV2Input().setUploadPartBasicInput(basicInput)
                            .setContentLength(data.length).setContent(content);
                    UploadPartV2Output output = tos.uploadPart(input);
                   
                    uploadedParts.add(new UploadedPartV2().setPartNumber(5).setEtag(output.getEtag()));
                    Log.i("uploadPart", "uploadPart succeed, partNumber is " + output.getPartNumber() + ", etag is " +
                                    output.getEtag() + ", crc64 value is " + output.getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException", "uploadPart failed");
                    e.printStackTrace();
                }

        
                try{
                    CompleteMultipartUploadV2Input complete = new CompleteMultipartUploadV2Input().setBucket(bucketName)
                            .setKey(objectKey).setUploadID(uploadID).setUploadedParts(uploadedParts);
                    CompleteMultipartUploadV2Output completedOutput = tos.completeMultipartUpload(complete);
                    Log.i("completeMultipartUpload", "completeMultipartUpload succeed, etag is " +  completedOutput.getEtag() +
                            ", crc64 value is " + completedOutput.getHashCrc64ecma() + ", location is " + completedOutput.getLocation());
                }catch (TosException e) {
                    Log.e("TosException", "completeMultipartUpload failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5Y-W5raI5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
## Cancel Multipart Upload Task

You can cancel a multipart upload by using the abortMultipartUpload interface. Once a multipart upload task is canceled, the corresponding uploadID can no longer be used for multipart uploads, and any parts that have already been uploaded will be deleted.

The following code demonstrates how to cancel a multipart upload.

```java
mport android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.AbortMultipartUploadInput;

public class AbortMultipartUploadExample extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";


        String uploadID = "the specific uploadID";
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    AbortMultipartUploadInput input = new AbortMultipartUploadInput().setBucket(bucketName)
                            .setKey(objectKey).setUploadID(uploadID);
                    tos.abortMultipartUpload(input);
                } catch (TosException e) {
                    if (e.getStatusCode() == 404) {
                        Log.e("TosException", "abortMultipartUpload failed, the specific upload id is not found");
                    } else {
                        Log.e("TosException", "abortMultipartUpload failed");
                    }
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5YiX5Li-5YiG54mH5LiK5Lyg5Lu75Yqh"></span>
## List Multipart Upload Tasks

You can use the listMultipartUploads operation to list multipart upload tasks that have been initialized via the createMultipartUpload interface but have not yet been completed or aborted. This interface returns a maximum of 1,000 multipart upload tasks per invocation. If the total number of tasks exceeds 1,000, you may call the interface repeatedly until all tasks have been listed.

<span id=".5Y-C5pWw6K-05piO"></span>
### Parameter Description

Parameter descriptions are provided below (all parameters below are optional).


|Parameters |Example |Definition |Usage |
|---|---|---|---|
|delimiter |/ |Character used to group object names. The '/' character is typically used as a grouping character. |new ListMultipartUploadsV2Input().setDelimiter(String delimiter) |
|encodingType |url |Specifies the encoding type for the returned content. The available values are described as follows:<br><br><br>* URL: Perform URL encoding. |new ListMultipartUploadsV2Input().setEncodingType(String encodingType) |
|maxUploads |100 |Returns the maximum number of multipart upload tasks, with an upper limit of 1,000; that is, a single request can return up to 1,000 multipart upload tasks. |new ListMultipartUploadsV2Input().setMaxUploads(int maxUploads) |
|prefix |aaa |Used to specify the prefix name for enumerating returned objects. This parameter can be used to organize and manage objects within the bucket by grouping them, similar to the functionality of folders. |new ListMultipartUploadsV2Input().setPrefix(String prefix) |
|keyMarker |test.txt |To be used in conjunction with uploadIDMarker. If uploadIDMarker is not specified, the list of multipart upload tasks whose object names are lexicographically greater than keyMarker will be returned. If uploadIDMarker is specified, the system returns a list of multipart upload tasks whose object names are lexicographically greater than keyMarker, as well as multipart upload tasks whose object name equals keyMarker and whose multipart upload task ID is greater than uploadIDMarker. |new ListMultipartUploadsV2Input().setKeyMarker(String keyMarker) |
|uploadIDMarker |f93f6fc9da94371f321e1008 |Used in conjunction with the keyMarker parameter. If keyMarker is not specified, ignore this parameter. If keyMarker is specified, the response includes the list of multipart upload tasks whose object names are lexicographically greater than keyMarker. Additionally, it returns multipart upload tasks where the object name equals keyMarker and the multipart upload task ID is greater than uploadIDMarker. |new ListMultipartUploadsV2Input().setUploadIDMarker(String uploadIDMarker) |


<span id=".56S65L6L5Luj56CB"></span>
### Sample Code

The following code demonstrates how to enumerate sharding tasks.

```java

import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.ListMultipartUploadsV2Input;
import com.volcengine.tos.model.object.ListMultipartUploadsV2Output;
import com.volcengine.tos.model.object.ListedUpload;

public class ListMultipartUploadsExample extends AppCompatActivity {
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
                    ListMultipartUploadsV2Input input = new ListMultipartUploadsV2Input()
                           
                            .setBucket(bucketName).setMaxUploads(10);
                    ListMultipartUploadsV2Output output = tos.listMultipartUploads(input);
                    Log.i("listMultipartUploads", "listMultipartUploads succeed, is truncated? " + output.isTruncated() + 
                            ", next uploadIDMarker is " + output.getNextUploadIdMarker() + ", next keyMarker is " + output.getNextKeyMarker());
                    if (output.getUploads() != null) {
                        for (int i = 0; i < output.getUploads().size(); i++) {
                            ListedUpload upload = output.getUploads().get(i);
                            Log.i("listMultipartUploads", "No." + (i + 1) + " listed upload is " + upload);
                        }
                    }
                } catch (TosException e) {
                    Log.e("TosException", "listMultipartUploads failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


The following code demonstrates how to paginate and list all ongoing shard tasks.

```java

import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.ListMultipartUploadsV2Input;
import com.volcengine.tos.model.object.ListMultipartUploadsV2Output;
import com.volcengine.tos.model.object.ListedUpload;

public class ListMultipartUploadsLoopExample extends AppCompatActivity {
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
                    boolean isTruncated = true;
                    String keyMarker = "";
                    String uploadIDMarker = "";
                    int total = 0;
                    while (isTruncated) {
                        ListMultipartUploadsV2Input input = new ListMultipartUploadsV2Input()
                                
                                .setBucket(bucketName).setMaxUploads(1000)
                                .setKeyMarker(keyMarker).setUploadIDMarker(uploadIDMarker);
                        ListMultipartUploadsV2Output output = tos.listMultipartUploads(input);
                        Log.i("listMultipartUploads", "listMultipartUploads succeed, is truncated? " + output.isTruncated() +
                                ", next uploadIDMarker is " + output.getNextUploadIdMarker() + ", next keyMarker is " + output.getNextKeyMarker());
                        if (output.getUploads() != null) {
                            for (int i = 0; i < output.getUploads().size(); i++) {
                                ListedUpload upload = output.getUploads().get(i);
                                Log.i("listMultipartUploads", "No." + (i+1+total) + " listed upload is " + upload);
                            }
                            total += output.getUploads().size();
                        }
                        isTruncated = output.isTruncated();
                        keyMarker = output.getNextKeyMarker();
                        uploadIDMarker = output.getNextUploadIdMarker();
                    }

                } catch (TosException e) {
                    Log.e("TosException","listMultipartUploads failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5YiX5Li-5bey5LiK5Lyg55qE5YiG54mH"></span>
## List Uploaded Chunks

You can use the listParts API to enumerate the parts that have been uploaded under the specified uploadID. This interface returns a maximum of 1,000 uploaded parts per call. If the total number of parts exceeds 1,000, you may invoke the interface repeatedly until all parts have been listed.

The following code demonstrates how to easily list the uploaded parts.

```java

import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.ListPartsInput;
import com.volcengine.tos.model.object.ListPartsOutput;
import com.volcengine.tos.model.object.UploadedPartV2;

public class ListPartsExample extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        
       
   
        String uploadID = "the specific uploadID";
       
        String objectKey = "your object key";
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    ListPartsInput input = new ListPartsInput()
                            
                            .setBucket(bucketName).setKey(objectKey).setUploadID(uploadID);
                    ListPartsOutput output = tos.listParts(input);
                    Log.i("listParts", "listParts succeed, is truncated? " + output.isTruncated() +
                            ", next partNumber marker is " + output.getNextPartNumberMarker());
                    if (output.getUploadedParts() != null) {
                        for (int i = 0; i < output.getUploadedParts().size(); i++) {
                            UploadedPartV2 upload = output.getUploadedParts().get(i);
                            Log.i("listParts", "No." + (i + 1) + " uploaded part is " + upload);
                        }
                    }
                } catch (TosException e) {
                    Log.e("TosException", "listParts failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


The following code demonstrates how to paginate the listing of all uploaded parts.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.ListPartsInput;
import com.volcengine.tos.model.object.ListPartsOutput;
import com.volcengine.tos.model.object.UploadedPartV2;

public class ListPartsLoopExample extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
      
       
    
        String uploadID = "the specific uploadID";
       
        String objectKey = "your object key";
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    boolean isTruncated = true;
                    int partNumberMarker = 0;
                    int total = 0;
                    while(isTruncated) {
                        ListPartsInput input = new ListPartsInput().setBucket(bucketName).setKey(objectKey)
                                
                                .setUploadID(uploadID).setPartNumberMarker(partNumberMarker);
                        ListPartsOutput output = tos.listParts(input);
                        Log.i("listParts", "listParts succeed, is truncated? " + output.isTruncated() +
                                ", next partNumber marker is " + output.getNextPartNumberMarker());
                        if (output.getUploadedParts() != null) {
                            for (int i = 0; i < output.getUploadedParts().size(); i++) {
                                UploadedPartV2 upload = output.getUploadedParts().get(i);
                                Log.i("listParts", "No." + (i+1+total) + " uploaded part is " + upload);
                            }
                            total += output.getUploadedParts().size();
                        }
                        isTruncated = output.isTruncated();
                        partNumberMarker = output.getNextPartNumberMarker();
                    }
                } catch (TosException e) {
                    Log.e("TosException", "listParts failed");
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


* For documentation on creating multipart upload tasks via the API, refer to [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload).

* For documentation on the API for uploading parts, see [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart).

* For API documentation on merging parts, refer to [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload).

* For API documentation on aborting multipart upload tasks, refer to [AbortMultipartUpload](https://docs.byteplus.com/docs/tos/reference-abortmultipartupload).
