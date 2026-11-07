---
title: "Delete service"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Delete_service"
---

If a service is no longer in use, the user can choose to delete the service.

<span id="使用前提"></span>
## premise of use


1. There are \> = 1 services in [inference services].

2. The service to be deleted needs to be stopped in advance and can only be deleted when the status is `not running`.


<span id="操作步骤"></span>
## Procedure


1. Log in to the Machine Learning Platform and click [Model Services] \- [Inference Services] in the left navigation bar to enter the list page. In the Actions area click 【···】\-【 Delete].

   * If the service is not bound to a public IP, a service will be deleted after a second confirmation.

   * If the service is bound to a public IP, you need to pay attention when deleting:

      * Delete service: Only delete the service, the public IP is still under the account and continues to be billed.

      * Delete service and public IP: When the corresponding public IP is no longer needed, click this button to delete the public IP bound to the service.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/823248d123c74490a61bcf3c040797cc~tplv-goo7wpa0wc-image.image" width="303px" /></div>



2. Click a service name on the list page to enter the details page, and click 【···】\-【 Delete] in the upper right corner to trigger the deletion operation.
