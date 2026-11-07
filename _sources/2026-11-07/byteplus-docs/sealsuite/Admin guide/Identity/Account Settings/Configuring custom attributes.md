---
title: "Configuring custom attributes"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-custom-attributes"
---

This article explains how to configure custom attributes in the Admin Console for employee information, in addition to the default system\-provided basic attributes.

<span id="0525cdca"></span>
## Adding custom attributes


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity**  **\> Account Setup**.

3. Go to the **Advanced settings** tab, and click  **+Add Field**.

   If you are using this function for the first time, you can check the pre\-filled name **Work Email**. This field supports edition and deletion.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/071d65a105aa42dc9f503e46b39d13aa~tplv-goo7wpa0wc-image.image) </span>

4. Fill in the information in the prompt box and click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e765cf82e3e499e97fe0e8753f3fbf9~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Field Key** |Set a unique key for the custom attribute. Field Keys cannot be repeated. |
   |**Field Name** |Give the custom attribute a name. |
   |**Description** |Give the custom attribute an introduction. |
   |**Field Type** |Choose the support type: String, Number, Boolean, Expression, or Enum.<br><br><br>* If you choose **String**, you need to configure **Default value** and **Advanced Configuration** (Required, Unique, Editable).<br><br>* If you choose **Number** or **Boolean**, you need to configure **Default value** and **Advanced Configuration** (Required, Editable).<br><br>* If you choose **Expression**, you need to configure the value of the expression and **Advanced Configuration** (Required).<br><br>* If you choose **Enum**, you need to configure:<br><br>   * Select **Multiple choice** or **Single selection**.<br><br>   * **Options**: Set the Enum key and name. You can set multiple keys by clicking  **+Add**.<br><br>   * **Default value**: Select one of the values as the default.<br><br>   * **Advanced Configuration**: **Required** or **Editable**. |
   |**Advanced Configuration** |The options are **Required, Unique, Editable**, and support multiple selections.<br><br><br>* **Required**: When selected, this attribute is a required field of employee information. Whether you create employee information or edit employee information, you need to configure this field value.<br><br>* **Unique**: When selected, it means that the attribute key is unique. If the field is configured with a default value, it is not allowed to be set as unique.<br><br>* **Editable**: When selected, it means that you can edit the field value within the employee information. |
   


<span id="1de17458"></span>
## Managing custom attributes


1. Log in to the Admin Console.

2. In the left navigation bar, click **Identity**  **\> Account Setup**.

3. Go to the **Advanced settings** tab, and you can view the values for existing custom attributes in the list, and click **Edit** or **Delete** to adjust the attribute.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7c36f5ffbcd4b20961e68a882ef6d90~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please proceed with caution when deleting a custom attribute, because the custom attribute cannot be restored after being deleted if the custom attribute has been used when adding employee information.   </div>
