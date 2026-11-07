---
title: "Update/Copy Services/Deployment Notes"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Update_CopyServices_DeploymentNotes"
---

<span id="服务-部署更新"></span>
## Service/Deployment Updates


|Parameter |Parameter Description |
|---|---|
|update service |Service update capability Added support for "private network", "load balancing" and "port" changes.<br><br><br>* After updating the private network:<br><br>   * If the service or deployment has the load balancing service turned on, make sure to update it to load balance on the current private network, otherwise it will not be available.<br><br>   * Also ensure that the subnet and SecurityGroup in the deployment complete the synchronous changes, otherwise the deployment will not be available.<br><br>* Update the load balancer/port, expect 2\-3 minutes without data inference requests. |
|update deployment |The ability to deploy updates adds support for "subnet", "SecurityGroup", "deploy independent load balancing", and "port" changes.<br><br><br>* Updating subnet/SecurityGroup triggers rolling service updates, but data inference requests are not interrupted.<br><br>* Update the load balancer/port, expect 2\-3 minutes without data inference requests. |


<span id="复制服务-部署"></span>
## Replication servicing/deployment


|Parameter |Parameter Description |
|---|---|
|replication service |Select the "Copy Service" operation to copy the "Basic Information" and "Service Network Configuration" information under the currently selected service. |
|replication deployment |After selecting "Replication Deployment", you can choose to replicate to a different service, and by default, replicate and add a new deployment to the current service.<br><br>After cross\-service replication is deployed, the settings of the target service's "private network", "load balancer" and "port" may conflict with the currently deployed "port", "load balancer", "subnet" and "SecurityGroup", requiring you to change and replace. |
