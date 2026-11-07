---
title: "Manage Tag Library"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Manage_Tag_Library"
---

The label library is used to upload and manage the label table. You can upload the local product dimension table (e.g. containing brand, product and other information for subject identification) and label dimension table (e.g. user consultation intention, operation intention and other information for label identification) to the label library through the label table template provided by the label library. These label tables can be referenced for marking when smart marking.

# Operation steps

1. In the left navigation bar of the **Enterprise Knowledge Engine** , select **Unstructured Marking** \> **Task Management** .

2. On the **Tag Library** page, click **New Tag Library**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0eee3e1265994287bc365ca080ce40d4~tplv-goo7wpa0wc-image.image)

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

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0e9ff551d5e4a60a1c674aa03eaee55~tplv-goo7wpa0wc-image.image)

   The following actions are available:

   * **Edit** : Go to the tag library details page and modify the configuration items.

   * **Recall test** : Enter the test page and enter keywords to test the similarity of the recalled content of the tag library.

   * **Delete** : Tag libraries that are no longer in use can be deleted and cannot be recovered after deletion.
