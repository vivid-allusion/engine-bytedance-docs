---
title: "Managing functions"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Managing_functions"
---

This article introduces how to manage functions, including online editing, code upload, image updating, function deletion, and more.

<span id="online-editing"></span>
## Online editing

Supports online editing of Node.js and Python code files.

After updating, you must re\-release the function for the changes to take effect.


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, find the target function and click the function name.

4. Switch to the code tab.

5. Click the version box in the top right corner, and select **Latest** version.

6. In the explorer area, click the file you want to edit.

7. Update the code as needed. After updating, click **Save**.


<span id="upload-code"></span>
## Upload code

The function service supports two code upload methods: local zip file upload and TOS upload. After uploading code, you need to re\-release the function for it to take effect.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before uploading code, please confirm that the code development has been completed locally.</div>


* <div data-tips="true" data-tips-type="tip">If using TOS upload, please confirm that you have activated and are using the BytePlus <a href="https://docs.byteplus.com/en/docs/tos/docs-what-is-tos">Torch Object Storage</a>.</div>


* <div data-tips="true" data-tips-type="tip">The code package must be a non\-encrypted zip file and must not exceed 256 MiB.</div>


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, find the target function and click the function name.

4. Switch to the code tab.

5. Upload code.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The Zip file uploaded here will overwrite all the code files currently in the editor.   </div>
   

   * **Upload local file**

      Click **Upload** \> **Upload local file** to upload the locally developed function code.

   * **Upload TOS**

      Click **upload** \> **Upload TOS** and, in the TOS upload panel, select the prepared storage Bucket and Zip file from the prerequisites.

6. Click **Confirm** to complete the code upload.


<span id="update-image"></span>
## Update image

For functions deployed through container images, support for updating the container images used by the functions is available. After the update, the function must be released again to take effect.


1. On the function list page, click the target function name to enter the current function's basic information tab.

2. In the **Function configuration** tab, edit the **Runtime**.

3. In the **Edit configuration information** panel, click **Modify image**.

4. On the pop\-up page, according to actual needs, select a new image version from the target image repository.

   When selecting images from the **Container Registry**, FaaS supports obtaining information such as **Startup command** and **Environment variables** from custom images. You can optionally choose whether to use the selected image's **Startup command** or **Environment variables** to override the current function's **Startup command** or **Environment variables**.

5. Click **Confirm**, return to the **Edit configuration information** panel.

6. After confirming the rest of the function configuration information, click **Save** to save the changes made to the function configuration.

7. Release the function to apply the changed configurations. For detailed operations, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).


<span id="delete-the-function"></span>
## Delete the function

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">After deleting the function, the function instance will be immediately released/destroyed, and the operation is irreversible. Please proceed with caution.</div>



1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. Select the region where your business is located in the top navigation bar.

3. On the **Function** page, select the target function, and click the  **`...`**  ** \> Delete** in the **Actions** column.

4. In the confirmation dialog that pops up, check the function information, then click **Delete** to delete the function.
