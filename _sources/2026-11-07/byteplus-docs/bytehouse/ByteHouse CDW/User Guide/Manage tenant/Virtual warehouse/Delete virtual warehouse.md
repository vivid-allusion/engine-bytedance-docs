---
title: "Delete virtual warehouse"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/delete-virtual-warehouse"
---

Delete a virtual warehouse when it is no longer needed. **This action will suspend all running searches**, meanwhile removing the virtual warehouse from the available list.

<span id="345ca767"></span>
## **Prerequisites**

Before running the delete operation, confirm that your current account has ALL permissions.

You can check the virtual warehouse permissions via **ByteHouse Console** \> **Access control** \> **User** \> **Username** \> **Resource privileges**. To obtain virtual warehouse param edit permission, contact the system administrator for configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ca8bae1208b494a970e49c472e01ed5~tplv-goo7wpa0wc-image.image) </span>

<span id="cab4b6e6"></span>
## Caution


* If the virtual warehouse to be deleted is set as the default write virtual warehouse, first switch or reconfigure the default write virtual warehouse as prompted by the interface, then run the delete operation.

* Deleting a virtual warehouse involves cost changes; you can refer to [Virtual warehouse unsubscription](https://docs.byteplus.com/docs/bytehouse/unsubscription#94a3657a) for details.


<span id="31a39ada"></span>
## Delete prepaid virtual warehouse

When unsubscribing from a subscription virtual warehouse, if there are elastic load resources in the virtual warehouse, the system deletes these elastic resources after successfully unsubscribing the basic resources of the virtual warehouse.


1. Log in to the ByteHouse console, under the **Virtual warehouse** tab, click the  **...**  button in the virtual warehouse list actions column. Click **Unsubscribe**, and the system will automatically jump to the BytePlus unsubscribe page.

2. After confirming the unsubscription information is correct, click confirm unsubscription to delete the virtual warehouse.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7e97f7e05bf4e6a924a41dbfd8553d6~tplv-goo7wpa0wc-image.image) </span>


<span id="1658808f"></span>
## Delete pay\-as\-you\-go virtual warehouse

When deleting a virtual warehouse, if there are any compute group elastic load resources, the system deletes the basic and elastic resources together.


1. Log in to the ByteHouse console, on the **Virtual warehouse** tab, click the **Delete** button in the actions column of the virtual warehouse list.

2. After confirming again in the popup confirmation box, you can delete the virtual warehouse.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/587eba9fdf524e4badaaa4e588589d9d~tplv-goo7wpa0wc-image.image) </span>


<span id="6827fcb1"></span>
## Next step: unsubscribe storage resources

After unsubscribing from the virtual warehouse, the storage resources in use will continue to be billed. If you no longer use ByteHouse Cloud Data Warehouse, please unsubscribe from both \*\*\*\* **virtual warehouse** and **storage** resources. For operation details, refer to [Storage resource cancellation](https://docs.byteplus.com/docs/bytehouse/unsubscription#16a0000d).
