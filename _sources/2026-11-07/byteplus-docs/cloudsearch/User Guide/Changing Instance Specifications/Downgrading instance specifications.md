---
title: "Downgrading instance specifications"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/downgrading"
---

When your instance configurations are higher than the configurations that your actual workloads need, consider downgrading node specifications to achieve better cost\-effectiveness.

<span id="c2b8fd53"></span>
## Precautions


* Downgrade is allowed only when the instance is in the **Running** state (indicated by green).

* Downgrading restarts instances. We recommend that you perform this operation during off\-peak hours.


<span id="2a21c924"></span>
## Procedure


1. Log into the [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Project and Region where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, find the desired instance, click `...` in the **Actions** column, and then choose **Downgrade**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab0ef8cd823243438ab6ea7371804958~tplv-goo7wpa0wc-image.image) </span>

4. In the dialog box that appears, confirm the message, and click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6d5aa7159e74a77a8a29bc5757f84a0~tplv-goo7wpa0wc-image.image) </span>

5. On the **Downgrade** page, modify the node specification configurations, and then click **Confirm order**.



|**Degradable Configuration Item** |**Description** |
|---|---|
|Node specification |The specifications of all types of nodes can be downgraded.<br><br>Different specifications correspond to varying numbers of vCPUs and memory. For more information on node specifications supported by Cloud Search, refer to [Specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Downgrading node specification results in node restart. Please perform this operation during off\-peak hours.</div><br> |



6. On the **Order details** page, check the change details, read and confirm the Terms of Service, and then click **Buy now**.

   Return to the **Instances** page to verify the operation. If the instance status is **Changing**, the operation is in progress. If the instance status is **Running**, the operation succeeds.
