---
title: "Changing the transfer protocol of an instance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/changing-transfer-protocol"
---

After you create an instance, you can enable or disable HTTPS to change its transfer protocol as needed.

<span id="9325e90d"></span>
## Precautions


* Changing the transfer protocol of an instance restarts the instance. To minimize service disruptions, we recommend that you perform this operation during off\-peak hours.

* If you change the protocol from HTTPS to HTTP, the instance will be accessible without security authentication and data will be transmitted in plain text over HTTP. In such cases, ensure that the access environment is secure and do not expose the access interface on the internet.


<span id="5a372959"></span>
## Procedure


1. Log into the [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Project and Region where the desired instance resides.

3. On the **Instances** page, click the name of the instance.

4. In the **Service access** pane of the **Basic** **information** page, toggle the HTTPS switch next to **Transport protocol**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To switch from HTTPS to HTTP, disable HTTPS.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To switch from HTTP to HTTPS, enable HTTPS.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The visualization platform Kibana or Dashboards has an independent HTTPS endpoint by default and is not affected by the instance transfer protocol.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f740b4825f0a42bb933193a74ec2e83d~tplv-goo7wpa0wc-image.image) </span>

5. In the dialog box that appears, read and confirm the precautions, and click **OK**.

6. View the operation progress.

   Return to the ** Instances** page to verify the operation. If the instance status is **Updating**, the operation is in progress. If the instance status is **Running**, the operation succeeds. This means that the protocol and address to access the instance have changed.
