---
title: "Adding custom attributes to devices"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-custom-attributes-to-devices"
---

SealSuite provides a set of default attributes for devices, but if additional attributes are required, you can import custom attributes beforehand. After a user installs and logs in to the SealSuite client, the system identifies the device using either the MAC address or the serial number. It then automatically populates the relevant fields with information about these custom attributes.

<span id="Procedure"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Assets** \> **Asset List**.

3. In the upper right corner of the page, click **Import Custom Attributes**.

   The **Batch Import** page will pop up.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4490166a32374f9292eb4d28695b96d0~tplv-goo7wpa0wc-image.image) </span>

4. At **Step 1**, click **Modify Configurations**.

   The **Modify Excel template fields** dialog box will pop up.

5. In the **Modify Excel template fields** dialog box, click **Add field**.

   The **Add Custom Attribute** dialog box will pop up.

6. In the **Add Custom Attribute** dialog box, fill in the blank fields by following the instructions below and click **OK**.

   
   |**Field** |**Description** |
   |---|---|
   |**Field name** |Customize the field name.<br><br>At the same time, you need to click the multilingual setting icon on the right side of the input field to configure the default display and English names. The default display name is required and will be displayed if no group name meets the selected language of the SealSuite client or the operating system. |
   |**Field type** |Select field type as **String**, **Boolean**, **integer**, **decimal**, **date**, or **Enum.**  |
   |**Enumeration value** |When you choose the **Field Type** as **Enum**, the Enumeration value appears. You need to fill in the Chinese and English of the enumeration values, and can click **Add** to add more enumeration values. |
   |**Is required** |Set this custom attribute as **Required** or **Not required**. |
   

7. At **Step 2**, select **MAC address** or **Serial** **number** to identify a device.

8. At **Step 3**, download the **Device import template** Excel file.

9. Open the **Device import template** file to fill in the device's MAC address or serial number, and customize custom attributes.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you added a custom attribute of enumeration value, the corresponding cell in the Excel template will be a drop\-down list. Ensure that the selected value exactly matches the enumeration value set in the Admin Console; otherwise, subsequent file upload may result in an error.   </div>
   

10. Return to **Step 4**, click **Upload** to upload the edited file.

11. At the bottom of the page, click **Confirm import**.

   After successful import, you can find the preset custom attributes in the **No device associated** group.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e0aaf5b9cc94a41a10ab315506066a6~tplv-goo7wpa0wc-image.image) </span>

   After a user installs and logs in to the SealSuite client on the device, the system will automatically populate the basic attributes along with preset custom attributes to improve the overall properties of the device. On the device details page, you can view the basic and custom attributes of the device.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c9ca56b7ab74b5389b12d059d4ccf4a~tplv-goo7wpa0wc-image.image) </span>
