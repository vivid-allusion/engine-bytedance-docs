---
title: "Create pipeline"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Create_pipeline"
---

<span id="相关概念"></span>
# Related concepts


* Custom training


<span id="使用前提"></span>
# Premise of use

When using a prepaid (proprietary) queue, have access to \> = 1 prepaid queue

<span id="操作步骤"></span>
# Procedure

The platform supports creating pipelines through the console (Web page) and SDK. Here is how to create pipelines through the console. For SDK creation, please check [Using the pipeline through the SDK](https://docs.byteplus.com/docs/mlp/Using_the_pipeline_through_the_SDK)


1. Log in to the Machine Learning Platform, click [Pipeline] in the left navigation bar, and enter the list page

2. Click [+ Create Pipeline] at the top left of the list page to enter the creation page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b16681fbb1e544cbb7e498ec02b604d3~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the basic information:



|Parameter |Parameter Description |
|---|---|
|Concept |* Fill in the name of the training task. **Required**<br><br>* Supports 1 to 200 visible characters, and only includes uppercase and lowercase letters, Chinese, numbers, dashes, and underscores. |
|Description |* Fill in the appropriate description of the pipeline. **Optional**<br><br>* Supports 1 to 500 visible characters. |



4. Configuration pipeline definition


Currently, only pipeline definitions through YAML are supported, and examples of single\-node pipelines are displayed by default in the YAML editor. For details on writing specifications, see [Define pipelines with YAML](https://docs.byteplus.com/docs/mlp/Define_pipelines_with_YAML).


* When you need to upload the code file of the node (subtask), you can click the [Insert Source Code] button, add the local file, and click [Upload]. The editor will upload the code to tos and insert the description file address into the current cursor of the YAML editor.

* The insert source tool will record the list of uploaded files during this editing process. If you need to reuse it, you can find the uploaded files in the description file address list and copy the description file address.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5acc24e7c4140eb8473a9520c59d160~tplv-goo7wpa0wc-image.image) </span>

   Click [Visualization] to preview the pipeline DAG diagram of the current YAML file configuration

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cdfcb6dfd99c4382bd0e3993e6096d11~tplv-goo7wpa0wc-image.image) </span>

5. Click [Confirm Creation], the YAML file passes the verification, and the pipeline can be created. After successful creation, it will jump to the latest configuration page of the pipeline.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24122635049e4f5ba116b00ebee5d0a0~tplv-goo7wpa0wc-image.image) </span>
