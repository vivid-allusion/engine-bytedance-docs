---
title: "GPU function management"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GPU_function_management"
---

This article introduces the basic actions for GPU functions, including: creating GPU functions, updating configuration information, updating images, deleting functions, and other operations.

<span id=".5Yib5bu6IEdQVSDlh73mlbA="></span>
## Create GPU functions

veFaaS supports creating GPU functions using container images. This article explains how to create GPU functions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use custom container image deployment, refer to <a href="https://docs.byteplus.com/en/docs/faas/Native_runtime">Native runtime</a> to complete code development, image building, and image pushing.</div>



1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar, click **Function \> Function management**.

4. On the **Function list** page, click **Create function** and select the target creation method. **Web applications**, **microservices applications**, and **tasks** all support container image deployment. Please select based on your actual business scenario.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Function name |Specify a custom name for the function. Function names cannot be repeated within the same account. After a function name is created, it cannot be modified. |
      |Description |Enter a description for the function. You can leave this field empty. |
      

   * **Function code**

      
      |**Parameter** |**Description** |
      |---|---|
      |Runtime |This scenario only supports **Native runtime**. |
      |Deployment method |Select **image** for this scenario.<br><br><br>* **Container Registry**: Select the specific image to deploy from your BytePlus Container Registry. You can filter out a specific image by instance, namespace, and repository type (public or private).<br><br>* **Public image**: Preconfigured images provided out\-of\-the\-box by veFaaS. Can be used directly, eliminating the need to develop code, build, and package images.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Public images are contributed by community developers. veFaaS does not maintain them. If you encounter any issues with using the software, please provide feedback to the community.</div><br> |
      

   * **Advanced settings**

      Only GPU\-related parameters are introduced here. For other parameter descriptions, see [Function configuration](https://docs.byteplus.com/en/docs/faas/Function_configuration).

      
      |**Parameter** |**Description** |
      |---|---|
      |Compute mode |Select **GPU acceleration** for this scenario. |
      |GPU card type |The following card types are currently supported:<br><br><br>* **NVIDIA A10** card type: Only a single card is supported. Video memory is 24 GB, memory specification is 112 GB. Suitable for deep learning inference scenarios and small\-scale training scenarios. Supports NVIDIA RTX™ features and provides high\-performance 3D graphics virtualization capabilities.<br><br>* **NVIDIA GPU** card type: Only a single card is supported. Video memory is 24 GB, memory specification is 60 GB. Suitable for generative AI inference and other large\-scale deployment scenarios. Supports NVIDIA RTX™ features and provides high\-performance 3D graphics virtualization capabilities. |
      

4. Click **Confirm** to complete the creation of the GPU function. After the function is created successfully, you can view it on the function list page.


<span id=".5pu05paw6YWN572u5L-h5oGv"></span>
## Update configuration information

Supports modifying information such as function execution timeout, single instance concurrency, environment variables, VPC network, and log delivery. After updating, you must release the function again for the changes to take effect.


1. On the function list page, click the target function name to enter the basic information tab of the current function.

2. Update configuration information, VPC network, and logs as needed.


<span id=".5pu05paw6ZWc5YOP"></span>
## Update image

Supports updating the container image used by the function. After updating, you must release the function again for the changes to take effect.


1. On the function list page, click the target function name to enter the basic information tab of the current function.

2. Switch to the code tab and click **Modify image**.

3. In the pop\-up confirmation box, click **Confirm**.

4. On the Modify image page, select the new image version from the target Container Registry.

5. Click **Confirm** to start updating the image.

   The system will synchronize the new image. Please wait.


<span id=".5Yig6Zmk5Ye95pWw"></span>
## Function deletion

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">After deleting the function, the function instances will be immediately released/destroyed. This action cannot be undone. Please proceed with caution.</div>



1. On the function list page, select the target function, and click **Actions** in the  **`...`**  column.  **\> Delete**.

2. In the confirmation dialog that pops up, verify the function information, and after confirming, click **Delete** to delete the function.
