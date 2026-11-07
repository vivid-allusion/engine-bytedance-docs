---
title: "Integrating VE SDK using Java"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/120-integrating-ve-sdk-using-java"
---

This section describes how to quickly integrate BytePlus Video Editor SDK using Java.

<span id="8e706bfd"></span>
# Prerequisites

Ensure you have imported the required dependencies.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are using <code>ComponentActivity</code> as your host instead of <code>FragmentActivity</code>, the Android runtime permission\-related interfaces provided in <code>EOQuickInitHelper</code> cannot be used. You can refer to the source code of <code>EOQuickInitHelper.kt</code>and implement them. For more information on requesting runtime permissions in Android, refer <a href="https://developer.android.com/training/permissions/requesting">here</a>.</div>


<span id="d5a34805"></span>
# Initialize the Application and SDK components using Java

This section introduces how to initialize the Application and SDK components using Java.

**To initialize the Application and SDK components**:


1. Create a class that is derived from the `Application` class.

   ```Java
   public class SampleApplication extends Application {
       @Override
       public void onCreate() {
           super.onCreate();
           ...
           EOQuickInitHelper.INSTANCE.setLicenseFileName("20231023_20241023_com.volcengine.effectone_union.licbag");
           EOQuickInitHelper.INSTANCE.initApplication(this);
       }
   }
   ```
   

2. Initialize the recording feature by referencing the following line of code:

   ```Java
   public class JavaActivity extends FragmentActivity {
       private View startRecordBtn;
       @Override
       protected void onCreate(@Nullable Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.main);
           startRecordBtn = findViewById(R.id.sample_start_recorder);
           startRecordBtn.setOnClickListener(new View.OnClickListener() {
               @Override
               public void onClick(View v) {
                   EOQuickInitHelper.INSTANCE.prepareAndInit(JavaActivity.this, new Function1<Boolean, Unit>() {
                       @Override
                       public Unit invoke(Boolean it) {
                           if (it) {
                               EOQuickInitHelper.INSTANCE.startRecorder(JavaActivity.this);
                           } else {
                               EOToaster.INSTANCE.show(JavaActivity.this, "Auth Fail", Toast.LENGTH_SHORT);
                           }
                           return null;
                       }
                   });
               }
           });
       }
   }
   ```
   

3. Initialize the export module.

   Currently, the Java source code of the export module is not provided in the demo project. You can develop your own export module for a Java project by referencing the Kotlin source code of the export page included in the demo project and the APIs for the export page. For more information, refer to [Initializing EOExportManager](https://docs.byteplus.com/docs/video-editor-sdk/120-initializing-eoexportmanager).
