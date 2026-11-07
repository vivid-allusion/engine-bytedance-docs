---
title: "Manage Label Library"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Manage_Label_Library"
---

The label library is used to upload and manage the label table. You can upload the local product dimension table (e.g. containing brand, product and other information for subject identification) and label dimension table (e.g. user consultation intention, operation intention and other information for label identification) to the label library through the label table template provided by the label library. These label tables can be referenced for marking when smart marking.

<span id="631a5a92"></span>
# Operation steps


1. Log into the Customer Data Platform and select **Smart Marking** \> **Tag Library** in the top menu bar.

   If the page width is insufficient, select **More** \> **Smart Marking** \> **Tag Library**.

2. On the **Tag Library** page, click **New Tag Library**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29eda1b1b2444a5d8b287ef64f74f65a~tplv-goo7wpa0wc-image.image) </span>

3. On the right side, **create a new tag library** interface, complete the following configuration, and click **Save** .

   * **Name** : Required, custom tag library name.

   * **Description** : Optional, custom tag library related information.

   * **Use scenario** : Required, you can choose **label recognition** and **subject recognition** .

      * If you select **tag recognition** , when the tag recognition application is configured in the smart marking task, the tag library can be selected for identifying the content related to the tag in the text.

      * If **subject recognition** is selected, when configuring the subject recognition application in the smart marking task, the tag library can be selected to identify the subject mentioned in the text.

   * **Tag library file** : Optional, upload the tag library file.

      * You need to download the **label recognition template** or **body recognition template** , populate the data in the format within the template and upload it.

      * You can create an empty tag library and then upload the tag library file, or you can upload the tag library file directly when creating.

4. (Optional) On the **Tag Library** page, view the tag library cards that have been created.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/355a637e99864be1bb73316e1b3e20e0~tplv-goo7wpa0wc-image.image) </span>

   The following actions are available:

   * **Edit** : Go to the tag library details page and modify the configuration items.

   * **Recall test** : Enter the test page and enter keywords to test the similarity of the recalled content of the tag library.

   * **Delete** : Tag libraries that are no longer in use can be deleted and cannot be recovered after deletion.
