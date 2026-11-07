---
title: "Managing access credentials"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing_access_credentials"
---

VKE enables you to manage cluster access credentials. This topic describes how to manage the KubeConfig access credentials for clusters.

<span id="kMEkPt83"></span>
## Considerations


* For each BytePlus root user and its IAM users, up to five KubeConfig files for private access and five KubeConfig files for public access can be generated in a single cluster. The quotas of a root user and its IAM users are counted separately. For more information about limits, see [Limit](https://docs.byteplus.com/en/docs/vke/Limits).

* When a cluster KubeConfig file is about to expire (with a validity period of less than 30 days), the system will report an event to the Cloud Monitor event center. You can configure an alerting rule for the KubeConfig file expiration event. For detailed instructions, see [Creating event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule).


<span id="rTuNlEAk"></span>
## Manage KubeConfig


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. On the **Overview** page, click the **Connection** tab to manage the cluster KubeConfig access credentials.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ca2c76fd5f732aae11494f584ac829e.png) </span>

   
   |No. |Feature |Description |
   |---|---|---|
   |① |Generate KubeConfig |Click **Generate KubeConfig**. Specify the **Valid period** and **Description** parameters, and then click **Confirm** to generate a new KubeConfig file for public access or private access. The Description parameter is optional. |
   |② |Copy KubeConfig |Copy the current KubeConfig file content to the temporary clipboard. |
   |③ |Download KubeConfig |Download the current KubeConfig file to your on\-premises computer. |
   |④ |Revoke KubeConfig |Revoke (delete) the current KubeConfig file.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Revoking a valid KubeConfig file is irreversible and will affect the connection to the related cluster. Proceed with caution.</div><br> |
   |⑤ |Manage KubeConfig |Manage and view the generated KubeConfig file within the current account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can view and manage the KubeConfig files generated within the current account and all its IAM users as a BytePlus root user.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · Apply for Trial</strong></a>] You can view all generated KubeConfig files in the current cluster as an IAM user granted cluster administrator permissions.</div><br> |
   |⑥ |Switch KubeConfig |You can switch to view the KubeConfig files generated within the current account. |
