---
title: "Progress Bar (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Progress-bar-android-sdk"
---

The SDK interfaces—putObject, appendObject, uploadPart, uploadFile, and getObject—all support progress bar functionality. You can pass in a custom interface to listen for events related to upload progress and implement custom business logic.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code uses putObject as an example to demonstrate how to use the progress bar feature.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.event.DataTransferListener;
import com.volcengine.tos.comm.event.DataTransferStatus;
import com.volcengine.tos.comm.event.DataTransferType;
import com.volcengine.tos.model.object.ObjectMetaRequestOptions;
import com.volcengine.tos.model.object.PutObjectBasicInput;
import com.volcengine.tos.model.object.PutObjectInput;
import com.volcengine.tos.model.object.PutObjectOutput;

import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;

public class PutObjectWithProgressExample extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        String endpoint = "your endpoint";
        String region = "your region";
        String accessKey = "your access key";
        String secretKey = "your secret key";
        String securityToken = "your security token";

        String bucketName = "bucket-example";
        String objectKey = "android-sdk-test-"+System.nanoTime();
        String filePath = getFilesDir().getPath() + "/test.txt";

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display_message);
        TOSV2 tos = new TOSV2ClientBuilder().build(region, endpoint, accessKey, secretKey, securityToken);

        Thread tosThread = new Thread(new Runnable() {
            @Override
            public void run() {
                DataTransferListener listener = new DataTransferListener() {
                    @Override
                    public void dataTransferStatusChange(DataTransferStatus dataTransferStatus) {
                        if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_STARTED) {
                            Log.i("putObject", "data transfer started.");
                        } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_RW) {
                            Log.i("putObject", "data transfer, sends " + dataTransferStatus.getRwOnceBytes() +
                                    " bytes once, has sent " + dataTransferStatus.getConsumedBytes() +
                                    " bytes, total bytes: " + dataTransferStatus.getTotalBytes());
                        } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_FAILED) {
                            Log.i("putObject", "data transfer failed, has sent bytes: " + dataTransferStatus.getConsumedBytes() +
                                    " , total bytes: " + dataTransferStatus.getTotalBytes());
                        } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_SUCCEED) {
                            
                            Log.i("putObject", "data transfer finishes, has sent bytes: " + dataTransferStatus.getConsumedBytes() +
                                    ", total bytes: " + dataTransferStatus.getTotalBytes());
                        }
                    }
                };
                try(FileInputStream inputStream = new FileInputStream(filePath)){
                    
                    ObjectMetaRequestOptions options = new ObjectMetaRequestOptions().setContentLength(new File(filePath).length());
                    PutObjectBasicInput basicInput = new PutObjectBasicInput().setBucket(bucketName).setKey(objectKey)
                            .setOptions(options).setDataTransferListener(listener);
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


The following code uses getObject as an example to demonstrate how to use the progress bar feature.

```java
import android.os.Bundle;
import android.util.Log;

import androidx.appcompat.app.AppCompatActivity;

import com.volcengine.tos.TOSV2;
import com.volcengine.tos.TOSV2ClientBuilder;
import com.volcengine.tos.TosException;
import com.volcengine.tos.comm.event.DataTransferListener;
import com.volcengine.tos.comm.event.DataTransferStatus;
import com.volcengine.tos.comm.event.DataTransferType;
import com.volcengine.tos.model.object.GetObjectV2Input;
import com.volcengine.tos.model.object.GetObjectV2Output;

import java.io.FileOutputStream;
import java.io.IOException;

public class GetObjectWithProgressExample extends AppCompatActivity {

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
                    DataTransferListener listener = new DataTransferListener() {
                        @Override
                        public void dataTransferStatusChange(DataTransferStatus dataTransferStatus) {
                            if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_STARTED) {
                                Log.i("getObject", "get object started.");
                            } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_RW) {
                                Log.i("getObject", "get object, read " + dataTransferStatus.getRwOnceBytes() +
                                                " bytes once, has read " + dataTransferStatus.getConsumedBytes() + 
                                                " bytes, total bytes: " + dataTransferStatus.getTotalBytes());
                            } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_FAILED) {
                                Log.i("getObject", "get object failed, has read bytes: " + dataTransferStatus.getConsumedBytes() +
                                        " , total bytes: " + dataTransferStatus.getTotalBytes());
                            } else if (dataTransferStatus.getType() == DataTransferType.DATA_TRANSFER_SUCCEED) {
                                
                                Log.i("getObject", "get object finishes, has read bytes: " + dataTransferStatus.getConsumedBytes() +
                                        ", total bytes: " + dataTransferStatus.getTotalBytes());
                            }
                        }
                    };
                    GetObjectV2Input input = new GetObjectV2Input().setBucket(bucketName).setKey(objectKey).setDataTransferListener(listener);
                   
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
