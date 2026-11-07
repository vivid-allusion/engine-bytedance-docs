---
title: "Resumable Upload (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume--android-sdk"
---

The SDK supports uploading large local files via the uploadFile resumable upload interface. During the uploadFile process, a checkpoint file will be recorded locally. If a network exception, program crash, or other similar situation causes the file upload to fail, invoking the interface again enables resumption of the upload from the progress recorded in the checkpoint file.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to upload files using the breakpoint resume interface.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.CreateMultipartUploadInput;
import com.volcengine.tos.model.object.UploadFileV2Input;
import com.volcengine.tos.model.object.UploadFileV2Output;

public class UploadFileExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";
        
      
        String uploadFilePath = "the path of file to upload";
      
        int taskNum = 5;
      
        long partSize = 10 * 1024 * 1024;
     
        boolean enableCheckpoint = true;
     
      
        String checkpointFilePath = "the checkpoint file path";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    CreateMultipartUploadInput create = new CreateMultipartUploadInput().setBucket(bucketName).setKey(objectKey);
                    UploadFileV2Input input = new UploadFileV2Input().setCreateMultipartUploadInput(create)
                            .setFilePath(uploadFilePath).setEnableCheckpoint(enableCheckpoint)
                            .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum);
                    UploadFileV2Output output = tos.uploadFile(input);
                    Log.i("uploadFile", "uploadFile succeed, object's etag is " + output.getEtag());
                    Log.i("uploadFile", "uploadFile succeed, object's crc64 is " + output.getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException","uploadFile failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5LqL5Lu255uR5ZCs5Yqf6IO9"></span>
## Event Listener Functionality

During the invocation of the uploadFile API, events such as chunk initialization, chunk upload, and chunk merge are triggered. You may pass in a custom interface to monitor relevant upload events and implement your own business logic.

The following code demonstrates how to utilize the event listener functionality.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.event.UploadEventType;
import com.volcengine.tos.model.object.CreateMultipartUploadInput;
import com.volcengine.tos.model.object.UploadEvent;
import com.volcengine.tos.model.object.UploadEventListener;
import com.volcengine.tos.model.object.UploadFileV2Input;
import com.volcengine.tos.model.object.UploadFileV2Output;

public class UploadFileWithEventListenerExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";

       
        String uploadFilePath = "the path of file to upload";
   
        int taskNum = 5;
      
        long partSize = 10 * 1024 * 1024;
        
        boolean enableCheckpoint = true;
       
        
        String checkpointFilePath = "the checkpoint file path";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    CreateMultipartUploadInput create = new CreateMultipartUploadInput().setBucket(bucketName).setKey(objectKey);
                    UploadEventListener listener = new UploadEventListener() {
                        @Override
                        public void eventChange(UploadEvent uploadEvent) {
                            if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventCreateMultipartUploadSucceed) {
                                Log.i("uploadFile", "event change, createMultipartUpload succeed");
                            }
                            if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventCreateMultipartUploadFailed) {
                                Log.i("uploadFile", "event change, createMultipartUpload failed");
                            }
                            if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventUploadPartSucceed) {
                                Log.i("uploadFile", "event change, uploadPart succeed");
                            }
                            if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventUploadPartFailed) {
                                Log.i("uploadFile", "event change, uploadPart failed");
                            }
                            if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventUploadPartAborted) {
                                Log.i("uploadFile", "event change, uploadPart aborted");
                            }
                            if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventCompleteMultipartUploadSucceed) {
                                Log.i("uploadFile", "event change, completeMultipartUpload succeed");
                            }
                            if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventCompleteMultipartUploadFailed) {
                                Log.i("uploadFile", "event change, completeMultipartUpload failed");
                            }
                        }
                    };
                    UploadFileV2Input input = new UploadFileV2Input().setCreateMultipartUploadInput(create)
                            .setFilePath(uploadFilePath).setEnableCheckpoint(enableCheckpoint)
                            .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum)
                            .setUploadEventListener(listener);
                    UploadFileV2Output output = tos.uploadFile(input);
                    Log.i("uploadFile", "uploadFile succeed, object's etag is " + output.getEtag());
                    Log.i("uploadFile", "uploadFile succeed, object's crc64 is " + output.getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException","uploadFile failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5pqC5YGc5oiW5Y-W5raI5pat54K557ut5Lyg"></span>
## Pause or Cancel Resumable Transfer

The uploadFile interface allows you to actively pause or cancel resumable upload tasks. Pausing a resumable upload task will halt the upload process. When uploadFile is invoked again, the upload can resume from the point where it was previously paused. Canceling a resumable upload task will halt the upload process, delete the local checkpoint file, and invoke abortMultipartUpload to remove the multipart upload task. If uploadFile is called again, the upload will restart from the beginning.

<SOURCE_TEXT\>The following code demonstrates how to pause or cancel a resumable transfer.</SOURCE_TEXT\>

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.event.UploadEventType;
import com.volcengine.tos.model.object.CreateMultipartUploadInput;
import com.volcengine.tos.model.object.UploadEvent;
import com.volcengine.tos.model.object.UploadEventListener;
import com.volcengine.tos.model.object.UploadFileV2Input;
import com.volcengine.tos.model.object.UploadFileV2Output;

public class UploadFileWithCancelExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";

       
        String uploadFilePath = "the path of file to upload";
      
        int taskNum = 5;
       
        long partSize = 10 * 1024 * 1024;
        
        boolean enableCheckpoint = true;
       
        
        String checkpointFilePath = "the checkpoint file path";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                try{
                    CreateMultipartUploadInput create = new CreateMultipartUploadInput().setBucket(bucketName).setKey(objectKey);
                    UploadFileV2Input input = new UploadFileV2Input().setCreateMultipartUploadInput(create)
                            .setFilePath(uploadFilePath).setEnableCheckpoint(enableCheckpoint)
                            .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum);
                   
                 
                  
                    boolean isAbort = true;
                    UploadEventListener listener = new UploadEventListener() {
                        @Override
                        public void eventChange(UploadEvent uploadEvent) {
                            if (uploadEvent.getUploadEventType() == UploadEventType.UploadEventUploadPartFailed) {
                                Log.i("uploadFile", "event change, uploadPart failed");
                                if (input.getCancelHook() != null) {
                                    
                               
                                   
                                    input.getCancelHook().cancel(isAbort);
                                }
                            }
                        }
                    };
                    input.setCancelHook(true).setUploadEventListener(listener);
                    UploadFileV2Output output = tos.uploadFile(input);
                    Log.i("uploadFile", "uploadFile succeed, object's etag is " + output.getEtag());
                    Log.i("uploadFile", "uploadFile succeed, object's crc64 is " + output.getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException","uploadFile failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```
