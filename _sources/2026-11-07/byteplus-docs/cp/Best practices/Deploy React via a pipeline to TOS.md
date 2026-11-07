---
title: "Deploy React via a pipeline to TOS"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Deploy_React_via_a_pipeline_to_TOS_object_storage"
---

This article describes how to use the pipeline feature in BytePlus Code Pipeline (CP) to quickly deploy front\-end applications to object storage TOS.

<span id="mzNWr4tz"></span>
## Prerequisites


* The React application has been brought under management in the code repository. In this example, Gitee is used as the repository.

* The artifact repository workspace has been created. For details about operations, refer to [create workspace](https://docs.byteplus.com/en/docs/cp/Create_a_workspace).


<span id="mzNWr4tz"></span>
## Procedure

<span id="I9nUpoR4"></span>
### Step 1: Create object storage


1. Log in to the [Object Storage Console](https://console.byteplus.com/tos). Create object storage.

   **Bucket policy**: select **Public read**. Fill in other parameters based on your business requirements. For configuration details, refer to [Create a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

2. Log in to the created storage bucket, then go to **basic configuration \-\>**  Create static network rules in the **Static Network** module. For details about Actions, refer to [Setting up a static website](https://docs.byteplus.com/en/docs/tos/Set-up-a-static-website).



|configuration |Descriptions |
|---|---|
|Default homepage |Enter site address. This example is `index.html`. |
|The default 404 page |Enter site address. This example is `index.html`. |



3. In **Domain and Transfer \-\> Custom Domain Name**, bind an ICP filed domain name to the bucket. For action details, refer to [Set custom domain name](https://docs.byteplus.com/en/docs/tos/Set-up-a-custom-domain-name).

4. Add DNS records for the domain in the [Cloud DNS Console](https://console.byteplus.com/dns-suite/dns). For operation details, refer to [Create a CNAME Record](https://docs.byteplus.com/en/docs/byteplus-dns-suite/9h8CZf).


<span id="40qpnI8L"></span>
### Step 2: Create a pipeline


1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp).

2. In the already created Code Pipeline workspace, create a code source and bring the React application code under management. For details about actions, refer to [Integrate code source](https://docs.byteplus.com/en/docs/cp/Integrate_code_source).

3. Create a **blank template** pipeline.

4. In the **code source & trigger** area, click **Add \-\> Code Source**. Add a managed code source.

5. Select the second pipeline node and reference the **NodeJS compile and build** task template.

6. In the **Step** area, click **add \-\> artifact \-\> TOS upload**.

7. Configure **TOS upload** parameters. For a detailed configuration description, refer to [TOS upload](https://docs.byteplus.com/en/docs/cp/TOS_upload).



|**Configuration Item** |**Descriptions** |
|---|---|
|Step name |By default, uploads are made to TOS, and you can customize step names. |
|Source file path |Upload file/folder path. The starting position must be a path relative to the project folder; wildcards are not supported. This example is for `build`: upload the build folder. |
|The TOS file path |Directory uploaded to TOS Bucket If the target directory does not exist, a directory will be created. This example is for`/`.<br><br><br>* `/`: Upload to the root directory of the Bucket.<br><br>* `demo/`: Upload to the demo directory in Bucket.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you upload a single file, for example, a.txt.</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If b is entered, the file will be renamed to b and uploaded to the root directory under Bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you enter b/, the file will be uploaded to the b directory under Bucket.</div><br> |
|Bucket region |Select the Region where the bucket to be uploaded is located. |
|Bucket name |Select the target Bucket for upload. |
|Include relative parent directory on upload |Do you want to upload together with the relative parent directory?<br><br><br>* Yes: The upload will include the parent directory and all contents within the directory.<br><br>* No: The upload content does not include the parent directory; only all contents within the directory are included. |
|Skip on failure |Optional configuration.<br><br><br>* Turn on: If the current Step fails, it will be skipped directly. The remaining Steps in the current task can continue to execute, and the pipeline will also continue to run.<br><br>* Turn off: If the current step fails, the remaining steps of the current task will not be executed, and the pipeline will fail. |



8. After modifications are complete, click **Save**, to finish creating,


<span id="xcIGmP5c"></span>
### Step 3: Run the pipeline


1. On the pipeline details page, click **Execute now**.

&nbsp;


<span id="GLA3ADP7"></span>
## Actions result

In the [TOS console](https://console.byteplus.com/tos), under the specified directory of a created bucket, view the uploaded files.

&nbsp;

<span id="uonKWFUK"></span>
## What to do next

<span id="cjplrMjs"></span>
### Access React static pages

After deployment is complete, you can access the React static page through a custom domain name that has been registered and filed.


1. In the [TOS console](https://console.byteplus.com/tos), view uploaded files in the specified directory of an already created bucket.

2. Obtain the custom domain name for static pages from the custom domain name list.

3. In the browser, enter **custom domain + site address,**  and the React page will be displayed. For example `https://cp-test-demo-*****/index.html`.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ae5eef08ddf23292c108ee72ce6d7c49.png) </span>
