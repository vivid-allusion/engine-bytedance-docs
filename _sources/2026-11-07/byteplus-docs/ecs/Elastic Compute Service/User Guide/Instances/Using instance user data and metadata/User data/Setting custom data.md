---
title: "Setting custom data"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuring-custom-data"
---

This topic describes how to set custom data for an ECS instance and verify its effects.

<span id=".6ZmQ5Yi26K-05piO"></span>
## Limits

The custom data for an instance must be encoded in Base64 format, and the data cannot exceed 16KB before Base64 encoding.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can enter custom data that has not been Base64\-encoded in the ECS console. The console will automatically perform Base64 encoding.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5YeG5aSH5a6e5L6L6Ieq5a6a5LmJ5pWw5o2u"></span>
### Step 1: Prepare custom data for the instance

Write a script that complies with specifications based on actual requirements. The recommended script formats vary for instances with different operating systems, as described in the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For sample scripts in different formats, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Configuring-custom-data#.6Ieq5a6a5LmJ5pWw5o2u6ISa5pys56S65L6L">Sample custom data scripts</a>.</div>



|Operating system |Script format |
|---|---|
|Linux |* Shell<br><br>* Cloud Config |
|Windows |* Batch<br><br>* PowerShell |


<span id=".5q2l6aqk5LqM77ya5bCG6Ieq5a6a5LmJ5pWw5o2u5Lyg5YWl5a6e5L6L"></span>
### Step 2: Pass custom data to the instance


<Tabs>
<Tab zoneid="gBLsVTFpaO" title="Pass in custom data when creating an instance">
<TabTitle>Pass in custom data when creating an instance</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After configuring custom data for an instance, this data will be executed when the operating system starts for the first time (including the first startup of the instance and the replacement of the operating system).</div>


When purchasing an instance, in the custom configuration phase, expand "Advanced Options" and enter the custom data for the instance. If the custom data of the instance is encoded in Base64 format, select "The text is encoded in Base64 format". Follow the on\-screen instructions step by step to create the instance.


</Tab>
<Tab zoneid="QyIifpdvKg" title="Modify custom data for an existing instance">
<TabTitle>Modify custom data for an existing instance</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Before modifying custom data, you must <a href="https://docs.byteplus.com/en/docs/ecs/Stopping-instances">stop the instance</a>. Otherwise, new data cannot be passed in.</div>


* <div data-tips="true" data-tips-type="default">After modifying custom data, as the instance status remains <strong>Stopped</strong>, you need to manually  <a href="https://docs.byteplus.com/en/docs/ecs/Starting-instances">start the instance</a>.</div>


* <div data-tips="true" data-tips-type="default">After the custom data is modified, whether the new custom data runs when you start the instance depends on the script type and module type, for example:</div>


   * <div data-tips="true" data-tips-type="default">Shell scripts: They will not run again, but only run when the operating system starts for the first time.</div>


   * <div data-tips="true" data-tips-type="default">Cloud Config scripts: If the configuration objects are modules such as Byobu or Set Passwords, they will not run again. They only run when the operating system starts for the first time.</div>


   * <div data-tips="true" data-tips-type="default">Cloud Config scripts: If the configuration object is the Update Etc Hosts module, they will run again every time the instance starts.</div>


      <div data-tips="true" data-tips-type="default">For more characteristics of module types, please refer to the individual modules and their module frequencies in <a href="https://cloudinit.readthedocs.io/en/latest/topics/modules.html?spm=a2c4g.11186623.0.0.45e46bd2Ba6Vsd">Modules</a>.      </div>
      

* <div data-tips="true" data-tips-type="default">When you modify an existing script, the previous content is displayed in the Custom data pane. By default, the script is not encoded in Base64.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the region and project.

4. Click the "··· \> Instance settings \> Change user data" button in the "Actions" column of the **stopped** instance.

5. Enter new custom data. If the instance custom data has been Base64\-encoded, please check the "The text is encoded in base64 format".

6. Click "Save" to complete the operation.


</Tab>
</Tabs>


<span id=".5q2l6aqk5LiJ77ya6aqM6K-B5Lyg5YWl5a6e5L6L55qE5YaF5a655ZKM6L-Q6KGM57uT5p6c"></span>
### Step 3: Verify the content and result passed to the instance


<Tabs>
<Tab zoneid="hYU7SWgUKK" title="Linux instance">
<TabTitle>Linux instance</TabTitle>

1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. View the content passed in from instance metadata.

   Run the following command to view the instance custom data as a root user. If the output matches the content passed in from[Step 2](https://docs.byteplus.com/en/docs/ecs/Configuring-custom-data#.5q2l6aqk5LqM77ya5bCG6Ieq5a6a5LmJ5pWw5o2u5Lyg5YWl5a6e5L6L), then the custom data has been successfully passed in the instance.

   ```Plain Text
   curl http://100.96.0.96/latest/user_data
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d68ae32ccc3af4f73d2e9d2737ff7d4.png) </span>

3. Run the following command to view the result of the instance custom data.

   The result depends on the content of the custom data. This topic takes writing specified content to the specified file userdata_test.txt as an example.

   ```Plain Text
   cat userdata_test.txt
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9e54155f8e1f0f2102fc9b0e566ccdb1.png) </span>


</Tab>
<Tab zoneid="SWlP59w3yc" title="Windows instance">
<TabTitle>Windows instance</TabTitle>

1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. View the passed\-in content from instance metadata.

   Run the following command as the root user to view the instance custom data. If the output matches the content passed in  [Step 2](https://docs.byteplus.com/en/docs/ecs/Configuring-custom-data#.5q2l6aqk5LqM77ya5bCG6Ieq5a6a5LmJ5pWw5o2u5Lyg5YWl5a6e5L6L), it indicates that the custom data has been successfully passed in the instance.

   ```Plain Text
   Invoke-RestMethod http://100.96.0.96/latest/user_data
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6b966dee8070443a191a172a818b4596.png) </span>

3. Verify the result.

   The result depends on the content of the custom data. This topic takes creating a file userdata_test.txt on the C drive as an example. Enter the C drive to view the result, as shown in the following figure.


</Tab>
</Tabs>


<span id=".6Ieq5a6a5LmJ5pWw5o2u6ISa5pys56S65L6L"></span>
## Custom data sample scripts

We recommend using the following script formats to set custom data. For more script formats, please refer to the [official cloudbase-init documentation](https://cloudbase-init.readthedocs.io/en/latest/userdata.html#powershell).


<Tabs>
<Tab zoneid="x7xzTHDkv8" title="Linux">
<TabTitle>Linux</TabTitle>

* **Shell**

   Starts with`#!`, such as`#!/bin/bash`, with no spaces at the beginning. The sample script is as follows:

   ```Plain Text
   #!/bin/bash
   echo "Hello World !" > /root/userdata_test.txt
   ```
   

* **Cloud Config**

   Starts with`#cloud-config`, with no spaces at the beginning. The sample script is as follows:

   ```Plain Text
   #cloud-config
   bootcmd:
   - echo "Hello World !" > /root/userdata_test.txt
   ```
   


</Tab>
<Tab zoneid="R5mesnuWQB" title="Windows">
<TabTitle>Windows</TabTitle>

* **Batch**

   Starts with `rem cmd`, with no spaces at the beginning. The sample script is as follows:

   ```Plain Text
   rem cmd
   echo "Hello World !" > C:\userdata_test.txt
   ```
   

* **PowerShell**

   Starts with `#ps1`, with no spaces at the beginning. The sample script is as follows:

   ```Plain Text
   #ps1
   echo "Hello World !" > C:\userdata_test.txt
   ```
   


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ModifyInstanceAttribute - Modifies instance information](https://docs.byteplus.com/en/docs/ecs/ModifyInstanceAttribute)

* [DescribeUserData - Queries instance's custom data](https://docs.byteplus.com/en/docs/ecs/DescribeUserData)
