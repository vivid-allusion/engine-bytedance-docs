---
title: "Using Function Service to achieve real-time automatic decompression of TOS uploaded files"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Using_Function_Service_to_achieve_real-time_automatic_decompression_of_TOS_uploaded_files"
---

This article introduces to you how to use Function Service (FaaS) to automatically decompress Zip files uploaded to Torch Object Storage (TOS) in real time.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenario introduction

In practical business scenarios, it is often needed to upload files to TOS for storage and use. To improve efficiency, the business side usually packs up all the files into a Zip archive to upload. However, in practical use, you still need to manually decompress the corresponding Zip archives, which is very inconvenient. Function Service combined with TOS Trigger can help you achieve real\-time automatic decompression of files after being uploaded to TOS to help you improve work efficiency.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Use restrictions


* It is recommended to avoid using Mac tools to compress files. If you must use the Mac tools to compress files, do not use Chinese characters in file names. Otherwise, this will cause the names of decompressed files to appear as garbled characters and the files cannot function properly.

* TOS Bucket and veFaaS functions must be in the same region.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* API Access Key

   Users have obtained the Access Key (AK and SK) of the current account and the key has TOSFullAccess. For specific operations, refer to [API Key Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys).

* Torch Object Storage

   * BytePlus TOS has been activated.

   * Create a bucket (TOS Bucket). For detailed operations, refer to [Creating a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* Function Service

   Function Service has been activated.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5L2_55So5Luj56CB5qih5p2_5Yib5bu65Ye95pWw"></span>
### Step One: Use code template to create the function

Use the code template **vefaas\-python39\-tos\-auto\-unzip** to create the function, and configure code information.


1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the function list page, click **Create function**.

4. On the Create function page, the major parameters are configured according to the following instructions, and the other parameters are configured as needed according to [Creating Event function](https://docs.byteplus.com/en/docs/faas/Creating_event_functions).

   
   |Parameter |Description |
   |---|---|
   |Function creation method |Select **Create [Event function]** . |
   |**Basic configuration** ||
   |Name |Customize the function name according to the naming rules prompted by the interface. After successfully creating the function, the name cannot be changed. |
   |**Function code** ||
   |Runtime |Select **Python 3.9**. |
   |Deployment method |Select **Function template** \> **vefaas\-python39\-tos\-auto\-unzip**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The template name can be viewed by clicking the <strong>Code preview</strong> option located under the <strong>Actions</strong> menu.</div><br> |
   

5. Click **Create** to complete creating the function.

   After successfully creating the function, the system will automatically redirect to the **Code** tab of the function details page.

6. On the **Code** tab of the function, the code template has provided the business code for automatic decompression. You only need to configure the following information.

   
   |Parameter |Description |
   |---|---|
   |ak |Enter the AK prepared in the prerequisites. |
   |sk |Enter the SK prepared in the prerequisites. |
   |endpoint |Enter the access domain of the intranet using the Endpoint (region node). |
   |region |Region. The TOS Bucket must be in the same region where the function is deployed. |
   |destination |This is the path where the Zip archive uploaded to TOS is stored after decompression. |
   

7. Click **Save** to save the modified code.


<span id=".5q2l6aqk5LqM77ya5Y-R5biD5Ye95pWw"></span>
### Step Two: Release the function

Release the current code and configuration of the function online.


1. On the function details page, click **Install dependencies** on the **Code** tab.

2. Once the dependencies finish installing，click **Release** in the upper\-right corner.

2. Use **Latest** for the **function revision**. Fill in the other parameters as needed or keep them at default values.

3. Click **Confirm** to start releasing the function. 


<span id=".5q2l6aqk5LiJ77ya6YWN572uIFRPUyDop6blj5Hlmag="></span>
### Step Three: Configure TOS Trigger

Configure the TOS Trigger for the current function and set the rules for triggering the function.


1. On the function details page, switch to **Trigger** tab, and click **Create Trigger**.

2. Configure the Trigger information as required. For more parameter details, refer to [Creating TOS Trigger](https://docs.byteplus.com/en/docs/faas/Creating_a_TOS_trigger).

   
   |Parameter |Description |
   |---|---|
   |Trigger type |Select the TOS Trigger. |
   |Trigger name |Customize the name of the Trigger according to the rules prompted by the interface. |
   |TOS Bucket |Select the TOS Bucket prepared in prerequisites. |
   |Trigger event |This example selects **tos:ObjectCreated:Put** and **tos:ObjectCreated:CompleteUpload**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the large file needs to be uploaded by different sections, select both <strong>tos:ObjectCreated:Put</strong> and <strong>tos:ObjectCreated:CompleteUpload</strong>. If you do not need to upload the large file by different sections, you can only select <strong>tos:ObjectCreated:Put</strong>, and execute triggering after uploading the object.</div><br> |
   |Filter conditions |By setting filter conditions, you can precisely match the object range of the events to be listened to, thus effectively lowering trigger frequency and reducing costs. This example sets the prefix as origin. That is to say, uploading a Zip archive to the `/origin` path triggers the automatic decompression of the uploaded task. |
   

3. Click **Confirm** to finish creating the TOS Trigger.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. On the **Trigger** tab of the current function, select the TOS Trigger created earlier. Click the name of Bucket to redirect to the corresponding Bucket in the TOS console.

2. Enter the `origin/` directory, click **Upload file** to submit a Zip archive locally.

3. Enter the `uncompressed/` directory and you can see the uploaded file is successfully unzipped to the `uncompressed/origin` directory.
