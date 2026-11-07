---
title: "Manage upstream version of Vital Kubernetes Engine type"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Managing_Upstream_Versions_of_Container_Service_Types"
---

For VKE type Upstream, you can configure different canary versions based on workload labels on the VKE side. This enables traffic management within and across clusters, supporting multi\-version management for applications.

<span id=".5re75YqgIFVwc3RyZWFtIOeJiOacrA=="></span>
## Add upstream version

Configure the corresponding canary label based on the workload label on the VKE side.


1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig), and in the top navigation bar, select the target region.

3. After selecting the target instance in **Instance Management**, click **Upstream list**. On the Upstream list page, click the target Upstream name to enter the current Upstream overview page.

3. In the canary label region, click **Add a canary label**. In the pop\-up dialog for adding a new canary label, set the version information.

   
   |Parameter |Description |
   |---|---|
   |Canary version |Customize the name of the current version. It is recommended to use a version name that is clear and easy to read. Canary version names must be unique within each Upstream. |
   |Tag |Enter the label (key:value) corresponding to the current version in the VKE system. You need to select a key\-value pair in the `spec.template.metadata.labels` parameter of the Deployment YAML as the basis for distinguishing the current version.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Please make sure the label is correct. Incorrect label entry will prevent traffic from being forwarded to the current version.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Only one canary label can be configured for the same label.</div><br> |
   

4. Click **Confirm** to complete the canary label configuration.


<span id=".57yW6L6RwqBVcHN0cmVhbSDniYjmnKw="></span>
## Edit upstream version

To modify a workload's label on the VKE side, you must also update the label corresponding to the current canary version on the gateway side.


1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig). In the top navigation bar, select the target region.

3. After selecting the target instance in **Instance Management**, click **Upstream List**. On the Upstream list page, click the target Upstream Name to enter the current Upstream Overview page.

3. In the canary label table, choose the canary label to be modified, and click the **actions** column's **Edit** button.

4. After modifying the key\-value pairs of the label, click **Confirm**.


<span id=".5Yig6ZmkIFVwc3RyZWFtIOeJiOacrA=="></span>
## Delete upstream version

If the workload label on the VKE side has been abandoned or deleted, you can delete the current canary label.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting the canary label, you must delete all routes associated with the current canary label.</div>



1. Log in to the [API Gateway Console](https://console.byteplus.com/veapig). In the top navigation bar, select the target region.

3. After selecting the target instance in **Instance Management**, click **Upstream List**. On the Upstream list page, click the target Upstream Name to enter the current Upstream Overview page.

3. In the canary label table, select the canary label to be deleted, and click the **actions** column's **Delete** button.

4. In the pop\-up secondary confirmation dialog, click **Delete**. This will delete the current canary label.
