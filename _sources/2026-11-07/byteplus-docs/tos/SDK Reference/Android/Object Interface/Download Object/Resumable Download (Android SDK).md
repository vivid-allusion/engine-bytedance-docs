---
title: "Resumable Download (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume-download-android-sdk"
---

When downloading large files, the downloadFile resumable download interface can be used. The TOS SDK enables concurrent segmented downloads of large files by utilizing the Range download method, and employs a local checkpoint mechanism to record successfully downloaded segments. If a download is interrupted due to network anomalies or machine failures, this interface may be invoked again to enable resumption.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to perform resumable downloads of large objects.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.model.object.DownloadFileInput;
import com.volcengine.tos.model.object.DownloadFileOutput;
import com.volcengine.tos.model.object.HeadObjectV2Input;

public class DownloadFileExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";

        
      
        String downloadFilePath = "the path of file to download";
        
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
                    HeadObjectV2Input head = new HeadObjectV2Input().setBucket(bucketName).setKey(objectKey);
                    DownloadFileInput input = new DownloadFileInput().setHeadObjectV2Input(head)
                            .setFilePath(downloadFilePath).setEnableCheckpoint(enableCheckpoint)
                            .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum);
                    DownloadFileOutput output = tos.downloadFile(input);
                    Log.i("downloadFile", "downloadFile succeed, object's etag is " + output.getOutput().getHeadObjectBasicOutput().getEtag());
                    Log.i("downloadFile", "downloadFile succeed, object's crc64 is " + output.getOutput().getHeadObjectBasicOutput().getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException","downloadFile failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```


<span id=".5LqL5Lu255uR5ZCs5Yqf6IO9"></span>
## Event Listening Functionality

During the invocation of the downloadFile interface, events such as creating temporary files, downloading file segments, and renaming temporary files are triggered. You can pass in a custom interface to monitor these download\-related events and implement your own business logic.

The following code demonstrates how to utilize the event listener functionality.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.event.DownloadEventType;
import com.volcengine.tos.model.object.DownloadEvent;
import com.volcengine.tos.model.object.DownloadEventListener;
import com.volcengine.tos.model.object.DownloadFileInput;
import com.volcengine.tos.model.object.DownloadFileOutput;
import com.volcengine.tos.model.object.HeadObjectV2Input;

public class DownloadFileWithEventListenerExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";

        
        
        String downloadFilePath = "the path of file to download";
       
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
                    HeadObjectV2Input head = new HeadObjectV2Input().setBucket(bucketName).setKey(objectKey);
                    DownloadEventListener listener = new DownloadEventListener() {
                        @Override
                        public void eventChange(DownloadEvent downloadEvent) {
                            if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventCreateTempFileSucceed) {
                                Log.i("downloadFile", "event change, createTempFile succeed");
                            }
                            if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventCreateTempFileFailed) {
                                Log.i("downloadFile", "event change, createTempFile failed");
                            }
                            if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventDownloadPartSucceed) {
                                Log.i("downloadFile", "event change, downloadPart succeed");
                            }
                            if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventDownloadPartFailed) {
                                Log.i("downloadFile", "event change, downloadPart failed");
                            }
                            if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventDownloadPartAborted) {
                                Log.i("downloadFile", "event change, downloadPart aborted");
                            }
                            if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventRenameTempFileSucceed) {
                                Log.i("downloadFile", "event change, renameTempFile succeed");
                            }
                            if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventRenameTempFileFailed) {
                                Log.i("downloadFile", "event change, renameTempFile failed");
                            }
                        }
                    };
                    DownloadFileInput input = new DownloadFileInput().setHeadObjectV2Input(head)
                            .setFilePath(downloadFilePath).setEnableCheckpoint(enableCheckpoint)
                            .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum)
                            .setDownloadEventListener(listener);
                    DownloadFileOutput output = tos.downloadFile(input);
                    Log.i("downloadFile", "downloadFile succeed, object's etag is " + output.getOutput().getHeadObjectBasicOutput().getEtag());
                    Log.i("downloadFile", "downloadFile succeed, object's crc64 is " + output.getOutput().getHeadObjectBasicOutput().getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException","downloadFile failed");
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

The downloadFile interface enables you to actively pause or cancel a resumable transfer task. Pausing a resumable download task will stop the download. When downloadFile is invoked again, the download can resume from the position where it was last paused. Canceling a resumable download task will stop the download and delete the local checkpoint file as well as any temporary files created during the download. If downloadFile is invoked again, the download will restart from the beginning.

The following code demonstrates how to pause or cancel a resumable transfer.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.event.DownloadEventType;
import com.volcengine.tos.model.object.DownloadEvent;
import com.volcengine.tos.model.object.DownloadEventListener;
import com.volcengine.tos.model.object.DownloadFileInput;
import com.volcengine.tos.model.object.DownloadFileOutput;
import com.volcengine.tos.model.object.HeadObjectV2Input;

public class DownloadFileWithCancelExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "your bucket name";
        String objectKey = "your object key";

        
        
        String downloadFilePath = "the path of file to download";
        
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
                    HeadObjectV2Input head = new HeadObjectV2Input().setBucket(bucketName).setKey(objectKey);
                    DownloadFileInput input = new DownloadFileInput().setHeadObjectV2Input(head)
                            .setFilePath(downloadFilePath).setEnableCheckpoint(enableCheckpoint)
                            .setCheckpointFile(checkpointFilePath).setPartSize(partSize).setTaskNum(taskNum);
                  
                   
                    boolean isAbort = true;
                    DownloadEventListener listener = new DownloadEventListener() {
                        @Override
                        public void eventChange(DownloadEvent downloadEvent) {
                            if (downloadEvent.getDownloadEventType() == DownloadEventType.DownloadEventDownloadPartFailed) {
                                Log.i("downloadFile", "event change, uploadPart failed");
                                if (input.getCancelHook() != null) {
                                    
                                    
                                   
                                    input.getCancelHook().cancel(isAbort);
                                }
                            }
                        }
                    };
                    input.setCancelHook(true).setDownloadEventListener(listener);
                    DownloadFileOutput output = tos.downloadFile(input);
                    Log.i("downloadFile", "downloadFile succeed, object's etag is " + output.getOutput().getHeadObjectBasicOutput().getEtag());
                    Log.i("downloadFile", "downloadFile succeed, object's crc64 is " + output.getOutput().getHeadObjectBasicOutput().getHashCrc64ecma());
                } catch (TosException e) {
                    Log.e("TosException","downloadFile failed");
                    e.printStackTrace();
                }
            }
        });

        tosThread.start();
    }
}
```
