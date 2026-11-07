---
title: "Manage model services"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Manage_model_services"
---

In personalization search scenarios, after developing a model, you can create a model service using the developed model. This topic describes how to manage model services.

<span id="Rhb7L5tQ"></span>
## Prerequisites


* A personalization search scenario has been created. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario).

* Data has been imported. For more information, see [Import data](https://docs.byteplus.com/en/docs/contextsearch/Import_data).

* Model development is complete, and the development task has run successfully. For more information, see [Model development](https://docs.byteplus.com/en/docs/contextsearch/Model_development).

* API Key created for calling model services. For more information, see [Create an API Key](https://docs.byteplus.com/en/docs/contextsearch/Create_an_API_Key).


<span id="yP56rXb8"></span>
## Create a model service


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the top\-right corner on the target personalized search and recommendation scenario page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>icon, select the **Model Service** tab, then click **Create Model Service**.

5. In the **Create model service** panel, configure the following parameters, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Development task |Select completed development tasks from the dropdown list. |
   |training record |Select the completed training record from the dropdown list. |
   |Service name |Set the name of the model service. Naming rules are as follows:<br><br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Length must be between 1 and 128 characters.<br><br>* Contain letters, digits, underscores (_), and hyphens (\-). |
   |Tag (optional) |Add tags to model services for easier identification and management. You can click **Add Tag** multiple times to add multiple tags, up to 20 tags in total. |
   |Description (optional) |Set the description for the model service. Length must not exceed 50 characters. |
   |Scenario resources ||
   |Resource type |Currently, only **CPU** is supported. |
   |Specification |Select the specification of the scenario resource from the dropdown list. |
   |Quantity |Set the quantity of scenario resources. Selectable quantity range: 1–200. |
   |Inference resource ||
   |Resource type |Currently, only **GPU** is supported. |
   |Specification |Select the specification of the inference resource from the dropdown list. |
   |Quantity |Set the quantity of inference resources. The selectable quantity is limited by the remaining stock of the chosen specification. |
   |Access point rate limiting |Turn on to set rate limiting for each access point. |
   |RPM |Turning on access point rate limiting requires configuring RPM (Requests Per Minute), which is the number of requests processed per minute. |
   |User\-defined parameter (optional) |Supports configuring user\-defined parameters for inference services. Click **Add custom parameters**, then configure the parameter name and value. |
   |recall fusion ratio |Turn on the recall fusion model as needed and specify the number of recalls.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is visible only when multiple recall model algorithms are specified in the model training configuration. For details, see <a href="https://docs.byteplus.com/en/docs/contextsearch/Model_development">Model development</a>.</div><br> |
   


<span id="rw3AwzEJ"></span>
## Start a model service

Model services must be started after creation before they can be called.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Only model services in <strong>Initializing</strong> or <strong>Stopped</strong> status can be started.</div>


* <div data-tips="true" data-tips-type="default">Only one model service can be started per personalization search and recommendation scenario.</div>


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the top\-right corner on the target personalized search and recommendation scenario page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>and select the **Model Service** tab, then click **start** in the **Running state** area.

5. In the popup dialog, click **OK**.


<span id="P2gOvV7h"></span>
## Invoke a model service

<span id="OW27pXjV"></span>
### Turn on model service access


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the top\-right corner on the target personalized search and recommendation scenario page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>icon, select the **Model Service** tab, and in the **access information** area, turn on **private network access** or **public network access** as needed.


<span id="gSuw6dSt"></span>
### Obtain invocation examples


1. Click **API access** in the upper right corner of the page.

2. In the **API Invocation** panel's **Select API Key** region, click **Quick fill API Key**.

3. In the pop\-up window, click **Select and fill** under the **Operation** column of the target API Key.

4. Copy the code in the **Select API Key** section and set the API Key as an environment variable.

5. Copy the code in the **Select call example** section to call the model service API.


<span id="8vfwwWMP"></span>
## Edit a model service


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the top\-right corner on the target personalized search and recommendation scenario page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>icon, then select the **model service** tab.

5. Click **Edit** in the **Scenario resource information**, **Inference resource information**, or **User\-defined parameters** section.

6. In the pop\-up dialog, modify the parameters as needed, then click **Save**. Please refer to [Create a model service](https://docs.byteplus.com/en/docs/contextsearch/Manage_model_services#yP56rXb8) for model service parameters.


<span id="um6HKl9w"></span>
## Grey release a model service

When the model development is complete and needs to be published, personalization search recommendation scenarios support grey release. You can verify by traffic proportion or designated account to achieve risk control and quick rollback.


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>icon  the top\-right corner on the target personalized search and recommendation scenario page, select the **Model service** tab, then click **Publish** in the top right corner.

5. In the **Grey release model service** panel, configure the following parameters, then click **Start grey release**.

   
   |Parameter |Description |
   |---|---|
   |Development task |Select the development task for the model service to be published from the dropdown list. |
   |Training record |Select the training record corresponding to the model service to be published from the dropdown list. |
   |Grayscale strategy |Select **Traffic canary** or **User canary**.<br><br><br>* Traffic grayscale: perform grayscale upgrade based on traffic proportion.<br><br>* User grayscale: perform grayscale upgrade for specified user IDs. |
   |Adjust grayscale traffic |Set the proportion of grayscale traffic for each stage. You can click **Add stage** to perform multi\-stage grayscale upgrade. This parameter is visible only when the **Grayscale strategy** is set to **Traffic grayscale**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The grayscale traffic proportion for the new stage must be higher than the previous stage.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The grayscale traffic proportion in the last stage cannot exceed 99%.</div><br> |
   |Set gray users |Set user IDs for grayscale upgrade. Separate multiple user IDs with commas or line breaks. |
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When not the first release, the <strong>Grey release model service</strong> dialog displays a comparison between current model evaluation indicators and online model indicators. If any core indicators fall below those of the online model, the system restricts publishing to prevent regression of the current online model’s performance.</div>


<span id="wErHDbYG"></span>
## Gradual upgrade of model service

Model services support gradual upgrades during model upgrades. You can verify by traffic percentage or designated accounts to control risk and enable quick rollback.


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the top\-right corner on the target personalized search and recommendation scenario page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>The **Model service** tab, then click **Gradual upgrade** in the **Associated models** area.

5. In the **Grey release** panel, configure the following parameters, then click **Start gray**.

   
   |Parameter |Description |
   |---|---|
   |Training record |Select the training record corresponding to the target model for upgrade from the dropdown list. |
   |Grayscale strategy |Select **Traffic canary** or **User canary**.<br><br><br>* Traffic grayscale: perform grayscale upgrade based on traffic proportion.<br><br>* User grayscale: perform grayscale upgrade for specified user IDs. |
   |Adjust grayscale traffic |Set the proportion of grayscale traffic for each stage. You can click **Add stage** to perform multi\-stage grayscale upgrade. This parameter is visible only when the **Grayscale strategy** is set to **Traffic grayscale**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The grayscale traffic proportion for the new stage must be higher than the previous stage.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The grayscale traffic proportion in the last stage cannot exceed 99%.</div><br> |
   |Set grayscale user |Set user IDs for grayscale upgrade. Separate multiple user IDs with commas or line breaks. |
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The <strong>Grey release</strong> dialog displays a comparison between the current model evaluation metrics and the online model metrics. If any core metric is lower than that of the online model, the system restricts the release to prevent performance regression of the current online model.</div>


<span id="QwxaAFv3"></span>
### Subsequent operations

After the canary upgrade starts, you can click **Associated model** area **Grey release upgrade history** and then check the canary upgrade progress in the **Grey release upgrade history** panel. Based on the upgrade status, choose **Urgent rollback** or **Proceed to the next canary upgrade stage**.

<span id="MAKqu1WB"></span>
## Restart a model service


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the icon at the top right of the target personalization search recommendation scene page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>Select the **Model service** tab, then click **Restart** in the **Running state** section.

5. In the popup dialog, click **OK**.


<span id="wtYH2ixN"></span>
## Delete model service


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>icon in the top\-right corner on the target personalized search and recommendation scenario page, select the **Model service** tab, then click **Delete** in the **Service basic information** section.

5. In the popup dialog, click **OK**.


<span id="j8zfsV2g"></span>
## Other configurations

<span id="NkEBxEym"></span>
### Turn on cache acceleration


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>icon in the top\-right corner on the target personalized search and recommendation scenario page, select the **Model Service** tab, then click the switch next to **Cache Acceleration** in the **Service Basic Information** section.

5. Configure the following parameters in the **Cache acceleration** dialog, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Cache acceleration |Turn on the cache acceleration switch. |
   |Redis instance |Select the Redis instance used for cache acceleration from the dropdown list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">To create a new Redis instance, see <a href="https://docs.byteplus.com/en/docs/redis/create-instance">Create an instance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For more information about Redis instances, see <a href="https://docs.byteplus.com/en/docs/redis/about-redis">What is Cache for Redis</a>.</div><br> |
   


<span id="LsfIIzT2"></span>
### Turn on access point rate limiting


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the top\-right corner on the target personalized search and recommendation scenario page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>Select the **Model Service** tab, then click the switch to the right of **Access Point Rate Limit** in the **Service Basic Information** section.

5. Configure the following parameters in the **Access point throttling** dialog, then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Cache acceleration |Turn on the access point rate limit switch. |
   |RPM |Set the maximum number of requests processed per minute. |
