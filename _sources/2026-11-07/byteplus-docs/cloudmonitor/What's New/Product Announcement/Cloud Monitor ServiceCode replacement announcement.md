---
title: "Cloud Monitor ServiceCode replacement announcement"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Cloud_Monitor_ServiceCode_replacement_announcement"
---

Due to the upgrade of the Cloud Monitor product architecture, the service name has been changed from `Volc_Observe` to `cloudmonitor`. The main impacts are as follows:


* If you have configured custom policies in the [Identity and Access Management (IAM) console](https://console.byteplus.com/iam) under **Permission policy**, and the policy includes configuration for the `Volc_Observe` service, please add the corresponding configuration for the `cloudmonitor` service as well.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To ensure compatibility, it is recommended that you do not delete the existing <code>Volc_Observe</code> service configuration, only add the new <code>cloudmonitor</code> service configuration.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The <code>cloudmonitor</code> service configuration has been added to the existing custom policy. You do not need to configure them again.   </div>
   

* When using OpenAPI, please use the Endpoint corresponding to `cloudmonitor`. For details, refer to [Service address](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address)
