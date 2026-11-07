---
title: "Scale up clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Scale_up_clusters"
---

When the computing resources or storage resources of an E\-MapReduce (EMR) cluster are insufficient, you can horizontally scale out the cluster. This article describes how to scale out a cluster.

<span id="_1-使用限制"></span>
## Limits

Only Core nodes and Task nodes can be scaled out, and the configuration of newly added nodes is identical to that of existing nodes by default.

<span id="_2-操作步骤"></span>
## Procedure


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?)

2. In the left navigation pane, click **Resource Management \> on ECS \> Cluster Details \>**  **Nodes,**  to go to the **Nodes** page.

3. Click the **Expansion** button in the operation column of the target node group.

4. In the scale\-out dialog box, configure the scale\-out settings and specify the number of nodes after scaling out.

5. Select the checkbox to agree to the E\-MapReduce service terms, and click the **Confirm** button to submit. The scale\-out operation is then complete.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the cluster is scaled out, some service parameters will be dynamically adjusted due to changes in cluster resources. Follow the prompts on the interface to restart the relevant services for the changes to take effect.   </div>
