---
title: "Managing files in ECS instances via Terminal"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Managing_files_in_ECS_instances_via_Terminal"
---

You can use Terminal to manage files on an ECS instance online. Terminal is suitable for scenarios such as remotely viewing text files, uploading deployment files, downloading diagnostic results, and organizing directories. This topic describes how to preview, upload, download, rename, and delete files in Terminal.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">This feature is currently in invite\-only beta testing. If you need to use it, please contact your account manager to apply.</div>


<span id="FBUOwIRz"></span>
## Prerequisites

The current account has the permissions to access and manage the target directory.

<span id="WGqoPnT4"></span>
## Preview files

<span id="AY6dzbUk"></span>
### Scenarios

When you need to quickly view configuration content, log snippets, or text scripts, you can preview files online without downloading them to your local computer first.

<span id="LKbBpRyc"></span>
### Instructions


* Only text files such as JSON, MD, and TXT are supported.

* The size of a single file preview cannot exceed 1 MB.


<span id="Fv9QOAtK"></span>
### Procedure


1. Log in to the ECS instance by [using Terminal (Linux) ](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance)or [Terminal (Windows)](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click "File management".

3. In the file list, find the target file and then click "Preview" in the Actions column.

4. View the file content in the preview pane.


<span id="MmjLIuIE"></span>
## Create folders

<span id="17YyOh9n"></span>
### Scenarios

If you plan to upload data files of different projects or categories, you can create multiple folders to store related files by category, so that the ECS instance can read files in the corresponding directories as needed for different tasks.

<span id="X4KHSNZD"></span>
### Procedure


1. Log in to the ECS instance by using [Terminal (Linux) ](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance)or [Terminal (Windows)](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click "File management".

3. On the file management page, click the "Create folder" button.

4. In the dialog box that appears, enter the folder name.

5. Click the "Confirm" button to complete the operation.


<span id="bxLkvcl0"></span>
## Upload files or folders

<span id="B4PPinEn"></span>
### Scenarios

To transfer deployment packages, scripts, configuration files, or directories to an ECS instance, you can upload files or folders directly in Terminal.

<span id="MLlZ2y6a"></span>
### Instructions


* You can upload a single file or a folder.

* You can pause, resume, or cancel an upload task.

* Multiple upload tasks are queued in the order of submission, and only one upload task runs at a time.

* If an exception occurs during the upload, the system prompts you to retry or cancel the operation.


<span id="dBUydcws"></span>
### Procedure


1. Log in to the ECS instance by using [Terminal (Linux)](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Terminal (Windows)](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click "File management".

3. Above the file list, click the "Upload" button and select "Upload file" or "Upload folder" as needed.

4. In the dialog box that appears, select the local file or folder that you want to upload to the ECS instance.

5. You can view the upload progress in the lower right corner. Before the upload is complete, you can also pause, resume, or cancel the task as needed.

   The progress window is a **file transfer list** that contains two modules: **upload tasks ** and ** download tasks**. After a file transfer is complete, the corresponding entry shows a progress indicator of 100%.


<span id="j50NNfX6"></span>
## Download the files

<span id="a6jBqsTJ"></span>
### Scenarios

When you need to save logs, exported results, or other files on the instance to your local computer, you can use the download feature.

<span id="NpvzFJiq"></span>
### Instructions


* A file of 20 MB or smaller triggers a browser download directly.

* When you download a file larger than 20 MB, the system displays a local storage window in which you can set the file name and select a save location.

* If the browser prevents you from saving the file to a restricted local path, change the save location as prompted, and then try again.


<span id="OCyTx6bP"></span>
### Procedure


1. Log in to the ECS instance by using[ Terminal (Linux)](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Terminal (Windows)](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click "File management".

3. On the file management page, click "Download" in the Actions column of the target file or folder.

4. The file is then automatically downloaded through your browser.


<span id="nsfXHT0G"></span>
## Rename a file

<span id="pI9RFQFX"></span>
### Scenarios

When you need to organize the directory structure or change file names, you can use the rename feature.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To keep your ECS instance running securely, you cannot rename its core files, such as system files and environment configuration files.</div>


<span id="W4aLHDQ6"></span>
### Procedure


1. Log in to the ECS instance by using [Terminal (Linux) ](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance)or [Terminal (Windows)](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click "File management".

3. On the file management page, locate the file or folder you want to rename, and click the "Rename" button in the "Actions" column.

4. Enter the new name in the pop\-up window ** and** click the "Confirm" button to complete the operation.


<span id="5dQG0zvv"></span>
## Delete a file

<span id="DXzXMkpc"></span>
### Scenarios

To clear unnecessary files, directories, or symbolic links, you can use the delete feature.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To keep your ECS instance running securely, you cannot delete its core files, such as system files and environment configuration files.</div>


* <div data-tips="true" data-tips-type="warning">After you delete a file, directory, or symbolic link, it cannot be recovered. Proceed with caution.</div>



<span id="lbFc3ac7"></span>
### Procedure


1. Log in to the ECS instance by using [Terminal (Linux)](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) or [Terminal (Windows)](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click "File management".

3. On the file management page, click "Delete" in the Actions column of the target file or folder.

4. In the dialog box that appears, confirm the risk information, and then click the "Delete" button to complete the operation.
