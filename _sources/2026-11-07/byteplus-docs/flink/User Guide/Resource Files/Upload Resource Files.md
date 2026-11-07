---
title: "Upload Resource Files"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Upload_Resource_Files"
---

The BytePlus Flink console offers unified management of resource files. The jar packages for developing JAR type tasks, Python ZIP packages for developing PyFlink tasks, and configuration files that the task depends on must be uploaded to the console in advance, essentially uploaded to the VCI container `/opt/tiger/workdir` directory.

<span id="03a87f38"></span>
## Prerequisites

Resource files are generally managed by developers (Project_Dev). Ensure the operator has been added as a project member and has an associated role, please refer [Add project members](https://docs.byteplus.com/docs/flink/Add_project_members).

<span id="69adccc8"></span>
## Upload resource files


1. Log in to [BytePlus Flink console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. In the left sidebar, select **Project Management**, perform a fuzzy search by project name in the search box, and then click on the project block to enter the project.

4. In the project’s left sidebar, select **File Management**, then click the Upload Resource button.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4336b4ed86cb4ae6b07bce7c61e77145~tplv-goo7wpa0wc-image.image) </span>


5. In the **Upload Resource** dialog, set the resource name and description, upload the file, and then click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b93bf22b3a1f4ac98b9f7df11c7450c4~tplv-goo7wpa0wc-image.image) </span>

Parameters for detailed configuration are as follows.


|**Configure** |**Explanation** |
|---|---|
|Resource File |Upload Local File.<br><br><br>* The name of the uploaded file can only consist of uppercase letters, lowercase letters, numbers, underscores (_), hyphens (\-), and periods (.).<br><br>* The file size must not exceed 100 MB. If the file is too large, it is recommended to use TOS object storage management.<br><br>* If a file is uploaded again, the new file will overwrite the previously uploaded file. |
|Resource Name |The default is to keep the same name as the file you uploaded, but you can customize and change the file name.<br><br>The file name can only consist of uppercase letters, lowercase letters, numbers, underscores (_), and periods (.), with a character length range of 1 to 60. |
|Resource Directory |Select the resource directory to which the resource file belongs.<br><br>The system has a default **default folder**, but to manage resource files more conveniently, you can freely create resource directories. |
|Resource Description |Fill in the description of the uploaded resource file, typically describing its function and use. |


<span id="f2bbe02c"></span>
## Manage resource files

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8235e2b074d34dbc9c50e598e19ed7db~tplv-goo7wpa0wc-image.image) </span>

After uploading resource files, the following operations are supported:


* View files: You can filter by file name, used resource directories, and other criteria. You can also easily view the TOS address where the file is located.

* Download files: Click **Download** to download the resource files to your local machine.

* Delete files: Click **Delete** to remove the resource files. Deleting resources is an irreversible operation. Please proceed with caution.
