---
title: "Using Function as a Service to read and write the TOS mounted directory"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Using_Function_Service_to_read_and_write_the_TOS_mounted_directory"
---

Mounting a TOS Bucket on a function enables persistent data storage and sharing across multiple functions. This article introduces how to use the BytePlus Function Service (FaaS) to read and write the mounted TOS Bucket.

<span id="w9INBifb"></span>
## Scenario introduction

Mounting a TOS Bucket on a function allows persistent data storage and sharing across multiple functions. In addition, functions can access TOS like a local file system, simplifying resource access and data processing.

<span id="LaYQNbPa"></span>
## Prerequisites


* Torch Object Storage (TOS)

   * The TOS is activated.

   * A TOS Bucket is created in the region where functions will be deployed. For detailed operation, refer to [Creating a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

   * API access keys are obtained, and the access keys are required to have permission to access TOS. Refer to  [API Key Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys) for specific operations.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To better manage permissions, it is recommended to use IAM user keys with minimal authorization. Avoid using BytePlus root user keys or IAM user keys with excessive permissions directly.   </div>
   

* Function Service (FaaS)

   The FaaS is activated.


<span id="CoMsehBd"></span>
## Procedure

<span id="EQFBsioT"></span>
### Step One: Create a function and mount TOS


1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the **function list** page, click **Create function** and select **Create [Event function]** .

   * Basic configuration

      Customize function name and remarks.

   * Function code

      * Runtime: Select **Python**.

      * Code template: Select **vefaas\-python38\-default**.

   * Advanced configuration

      Enable TOS mount feature for storage configurations, and keep other parameters as default.



|**Parameter** |**Description** |
|---|---|
|AKSK |Enter Access Key ID and Secret Access Key to authorize the FaaS to use TOS. The access key must have reading and writing permissions for TOS. |
|TOS mount |Add a TOS mount point. This example adds one TOS mount point.<br><br><br>* **Bucket**: Select the TOS Bucket to mount.<br><br>* **Access address**: Automatically obtained after selecting the Bucket.<br><br>* **Bucket subdirectory**: Select the Bucket subdirectory the function needs to access. Must start with/. This example is /docdemo.<br><br>* **Local directory**: Configure the local directory in the function operation environment. This example is /mnt/tos.<br><br>* **Permission**: This example selects reading and writing permissions, allowing the function to read and write the local directory mounted on the Bucket. |



4. Click **Create** to complete function creation.


<span id="QADbhtn9"></span>
### Step Two: Edit code online

This article uses the following code example to demonstrate to you how to read and write the mounted TOS Bucket.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The code logic is for reference only. Modify the code according to your actual business scenario as needed.</div>



1. On the Code tab of the current function, click index.py file, overwrite the original content with the following code, and click **Save**.


```Python
import json
import os

def handler(event, context):
    print(f"received new request, event content: {event}")

# Mount point local directory. Keep consistent with the actual situation.
mount_path = '/mnt/tos'# Read a file from the mount directory. Replace tos.txt with a file that exists in the mount directory in actual use.
    file_path = os.path.join(mount_path, 'tos.txt')
    if os.path.exists(file_path):
        with open(file_path, 'r') as file:
            content = file.read()
            print("Content of tos.txt:", content)
    else:
        print("tos.txt does not exist.")

# write a file to the mount directory.
    write_path = os.path.join(mount_path, 'output.txt')
    with open(write_path, 'w') as file:
        file.write("Hello, TOS mount!")
        print("Wrote to output.txt in TOS mount.")

    result = {
        'statusCode': 200,
        'headers': {
            'Content-Type': 'application/json'
        },
        'body': json.dumps({
            'message': 'Hello FaaS TOS mount!'
        })
    }
    return result
```


<span id="pNT7rQ1a"></span>
### Step Three: Release the function

Release the current code and configuration of the function online.


1. On the function details page, click **Release** in the upper\-right corner.

2. The function revision uses Latest. Keep other parameters as default.

3. Click **Confirm**. Wait for the function release to complete.


<span id="gsTxAV3Q"></span>
## Result validation


1. Test the function to verify whether the response result meets expectations.

   1. On the function details page, click **Test** in the upper\-right corner.

   2. On the pop\-up function test page, configure the Trigger type and test request.

      * Trigger type: Select API Gateway Trigger.

      * Test request: Keep the default.

   3. Click **Test**. Wait for the test results.

      As shown in the figure: The function returns the expected content, meeting expectations.

2. View the instance logs of the function to confirm whether the expected file reading and writing is completed.

   1. Switch to the Resource management tab.

   2. In the Instances list, select the running instance, click **Logs**, and enter the instance logs page.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When a function has multiple instances, it is recommended to check the logs of each instance to identify the one instance actually handling the request.   </div>
   

      As shown in the figure: The function returns the content of tos.txt under the TOS mount directory and writes the output.txt file in the TOS mount directory.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f365bbcf0bc9eda685819b3895b6944b.png) </span>

3. Log in to the TOS console and check whether the output.txt file is written under the corresponding mount directory.

   As shown in the figure: The output.txt file is written under the /docdemo directory of the target Bucket.


&nbsp;
