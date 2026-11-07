---
title: "Quickly create and use scenarios"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Quickly_create_and_use_scenarios"
---

ContextSearch offers a variety of scenario templates with built\-in common parameter configurations. You can create search scenarios with one click based on these templates to quickly complete the basic setup. This topic describes how to quickly create and use scenarios with scenario templates.

<span id="sNCnVgbq"></span>
## Quickly create scenarios


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, select **ContextSearch \> Home**.

4. Click **Create** on the scenario template card based on your needs. The currently supported scenario templates include **General knowledge base**, **General Image Search**, and **General Video Search**.

5. In the **Create scene** panel, configure the following parameters and then click **Create**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Set the name of the scene. Naming rules are as follows:<br><br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Length must be between 1 and 128 characters.<br><br>* Contain letters, digits, underscores (_), and hyphens (\-). |
   |Description (optional) |Description of the scene setup. Length must not exceed 255 characters. |
   |Affiliated project |Project to which the scene belongs. You cannot switch when creating a scene. To switch, close the dialog and modify it from the top navigation bar. |
   


<span id="uu8M0HIU"></span>
## Configure a scenario


1. On the scenario details page, some configurations are auto\-completed based on the template. Click **Configure** to set up storage and embedding.

2. In the **Basic configuration** dialog, set the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Storage location |Select the instance type for running the scene. Currently supports **specifying database instances**. |
   |Database type |Select the database type used by the scene. Currently supports **Cloud Search**. |
   |Instance name/ID |Select the target OpenSearch instance from the dropdown list. Supports fuzzy search based on keywords in the instance name. If a new OpenSearch instance is needed, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only OpenSearch version 2.9.0 instances support ContextSearch.</div><br> |
   |Authorize to use an instance |Display the instance authorization status. You can follow these steps to authorize full access for ContextSearch service to the OpenSearch instance.<br><br><br>1. Click **To authorize**.<br><br>2. In the **Instance authorization** dialog, enter the instance **username** and **password**, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Without authorization, the scenario cannot use the OpenSearch instance resources.</div><br> |
   |Private network |To ensure smooth intranet access, it is recommended to select the VPC in the region where your existing cloud services are located. Subnets in different availability zones within the same VPC can communicate with each other. If you want to create a VPC, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). |
   |Subnet |The system automatically filters available subnets based on the region, availability zone, and VPC that you select. If you want to create a new subnet, see [Creating a subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet). |
   |Model source |Select **Default model** or **Ark model**. |
   |Model/inference service |Select models associated with the created inference service. |
   |API Key |Select the API Key used to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/docs/6465/1359479). |
   


<span id="bkbqQObr"></span>
## add retrieval file

The scenario initializes automatically after configuration is complete. After initialization, you can add retrieval files.


1. After the scenario configuration is complete, click **Add** in the **Retrieve files** section.

2. In the **Add file** panel, perform the following, then click **OK**.

   1. Select **TOS** or **Local documentation**.

      * Object storage: Select the bucket and target folder containing the files to add. If there are no available buckets, please create a bucket first. For detailed steps, see [Creating a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

      * Local documents: Click the upload area to select files or drag files to the upload area, then wait for the upload to complete.

   2. (Optional) If you are creating a general video search scenario, configure the following parameters.

      
      |Parameter |Description |
      |---|---|
      |Speech recognition service model/inference service |Select whether to turn on the speech recognition service model/inference service. When turned on, configure the following parameters.<br><br><br>* Model/inference service: select the speech recognition model associated with the inference service.<br><br>* API Key: select the API Key used to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/docs/6465/1359479). |
      |Video understanding model |Select whether to turn on the video understanding model. After turning on, configure the following parameters.<br><br><br>* Model source: select **Default model** or **Ark model**.<br><br>* Model/inference service: select the video understanding model associated with the inference service.<br><br>* API Key: select the API Key used to call the model. If you need a new API Key, see [Create an API Key](https://docs.byteplus.com/docs/6465/1359479).<br><br>* Prompt (optional): enter a prompt for video understanding, such as "summarize video content". |
      |Maximum slice length |Set the maximum slice length for the video. You can choose 15 seconds, 30 seconds, 60 seconds, or a user\-defined length. |
      


<span id="o34TDqai"></span>
## Debug preview

After adding retrieval files, you can enter text and upload images in the **debug preview** area to test search results.

<span id="lf7zhqA2"></span>
##
