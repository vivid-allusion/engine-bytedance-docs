---
title: "Configure Large Model Invocation"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Configure_Large_Model_Invocation"
---

In the visual knowledge processing task, some AI operators implement corresponding data processing functions based on large models. Operators can choose from a large range of models that require enterprise administrators to add in advance in the console. This article describes how to add the large model required by the operator.

<span id="51bca62e"></span>
# Prerequisite

It is recommended that enterprise administrators maintain large model call settings. If an enterprise administrator needs to specify another user to maintain the large model call settings, they need to first grant that user **advanced configuration edit and view** permissions for **visual modeling, data sets**. Please refer to the specific operation instructions for authorization [Authorization Management](https://docs.byteplus.com/docs/dataagent/Authorization_Management__).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9a4098a19f64a5f9e9a7608325bc66c~tplv-goo7wpa0wc-image.image) </span>

<span id="abde1916"></span>
# Operation Steps


1. Log in to the Marketing Agent console.

2. Select **Enterprise Knowledge Engine** in the left navigation bar.

3. In the left navigation bar of Enterprise Knowledge Engine, select **Project Center** \> **Knowledge Processing Configuration**.

4. In the left navigation bar of the knowledge processing configuration, select **Advanced Settings** \> **Large Model Call Settings**.

5. On the **Large Model Call Settings** page, select the operator that needs to add the large model.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/171ca8b0da494a79b501061a87b90f67~tplv-goo7wpa0wc-image.image) </span>

6. Click **New Model** on the right side of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d044b5fae7424490bcade5b050d8a310~tplv-goo7wpa0wc-image.image) </span>

7. Complete the configuration item in the pop\-up window and click **OK**.

   Different operators require different configurations, and you need to configure them according to the actual interface information.

   
   |**configuration scenario** |**configuration item description** |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cfe4fb6752c4af99d707e7277384552~tplv-goo7wpa0wc-image.image) </span> |* **Model Name** : A custom name that identifies the current model.<br><br>* **Model call address** : the call address of the application.<br><br>* **Inference Access Point** : The general format is `ep-xxxxxxxxxx-yyyy`, and the creation method refers to [creating a custom inference access point ](https://www.volcengine.com/docs/82379/1099522).<br><br>* **API Key** : The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method refers to [obtaining API Key and configuring ](https://www.volcengine.com/docs/82379/1263279). |
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71354023034345f3be5976eb526bc140~tplv-goo7wpa0wc-image.image) </span> |* **Model Name** : A custom name that identifies the current model.<br><br>* **AppId** : App ID under the bean bag voice service, please refer to [how to get parameters App, Token, etc ](https://www.volcengine.com/docs/6561/196768?lang=zh#q1%EF%BC%9A%E5%93%AA%E9%87%8C%E5%8F%AF%E4%BB%A5%E8%8E%B7%E5%8F%96%E5%88%B0%E4%BB%A5%E4%B8%8B%E5%8F%82%E6%95%B0appid%EF%BC%8Ccluster%EF%BC%8Ctoken%EF%BC%8Cauthorization-type%EF%BC%8Csecret-key-%EF%BC%9F).<br><br>* **Access Token** : Access Token under the bean bag voice service, please refer to [how to get parameters App, Token, etc ](https://www.volcengine.com/docs/6561/196768?lang=zh#q1%EF%BC%9A%E5%93%AA%E9%87%8C%E5%8F%AF%E4%BB%A5%E8%8E%B7%E5%8F%96%E5%88%B0%E4%BB%A5%E4%B8%8B%E5%8F%82%E6%95%B0appid%EF%BC%8Ccluster%EF%BC%8Ctoken%EF%BC%8Cauthorization-type%EF%BC%8Csecret-key-%EF%BC%9F).<br><br>* **Resource Information ID** :<br><br>   * Bean Bag Recording File Recognition Model 1.0: volc.bigasr.auc<br><br>   * Bean Bag Recording File Recognition Model 2.0: volc.seedasr.auc |
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02d4fc78f42b43678a2b81e398f2ccd2~tplv-goo7wpa0wc-image.image) </span> |* **Model Name** : A custom name that identifies the current model.<br><br>* **Access Key ID** and **Secret Access Key** : The access key (AK/SK) of the Volcano Engine account that has opened the image recognition and understanding service. For the operation guide, please refer to:<br><br>   * [Open image recognition and understanding services](https://www.volcengine.com/docs/86081/1660346?lang=zh)<br><br>   * [API Access Key Management](https://www.volcengine.com/docs/6291/65568?lang=zh) |
   

8. Verify that the configuration is in effect.

   1. After the model is added, the model list of the operator supports viewing configuration information, **editing** or **deleting** operations.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Once the model is deleted, it cannot be restored. Please proceed with caution.      </div>
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebf9b9f96c9849bc9938f2012e6f8506~tplv-goo7wpa0wc-image.image) </span>

   2. Create a test task that previews the added models in the corresponding operator configuration.

      How to create a task, see [Step 1: Create a new task](https://docs.byteplus.com/docs/dataagent/Offline_Task#0dbb27de).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e2350ed08ff4ccda9c4add69db6fffd~tplv-goo7wpa0wc-image.image) </span>
