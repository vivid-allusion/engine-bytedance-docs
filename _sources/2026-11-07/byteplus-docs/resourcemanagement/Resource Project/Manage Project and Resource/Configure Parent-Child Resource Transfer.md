---
title: "Configure Parent-Child Resource Transfer"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Configure_Parent-Child_Resource_Transfer"
---

You can enable the parent\-child resource transfer feature. After the feature is enabled, the transfer of a parent resource to another project triggers the transfer of the child resource to the same project. This ensures that the parent and child resources are always in the same project.

<span id="scenario-examples"></span>
## Scenario examples


1. The child resources associated with a cloud server instance include cloud drives, NICs, and elastic IP addresses. When a cloud server instance is transferred to another project, the child resources associated with the instance are automatically transferred to the project where the instance is located. However, the transfer of child resources does not affect the parent resources. It means cloud drives, NICs, and elastic IP addresses can be independently transferred to other projects without changing the project to which the cloud server instance belongs.

2. The child resources associated with a private network routing table include routing entries. When the private network routing table is transferred to another project, the child resources associated with the routing table are automatically transferred to the project where the routing table is located. To avoid the impact on the business caused by the routing table and its associated routing entries not being in the same project, routing entries are prohibited from independent transfer and can only be transferred along with the routing table.


<span id="viewing-supported-parent-and-child-resources"></span>
## Viewing supported parent and child resources


1. Go to Access control \> [Resource project](https://console.byteplus.com/iam/resourcemanage/projectsettings).

2. Click Project settings.

3. The list displays the supported parent and child resources. Note:

   1. Once enabled, the configuration of parent and associated child resources will take effect globally under the account.

   2. The independent transfer prohibition identifier indicates that the child resource of this type cannot be directly transferred to another project. The configuration becomes invalid after being disabled.


<span id="enabling-disabling-parent-and-child-resources"></span>
## Enabling/Disabling parent and child resources


1. Go to Access control \> [Resource project](https://console.byteplus.com/iam/resourcemanage/projectsettings).

2. Click Project settings. You can enable or disable the transfer of some parent and child resources.

3. When it is enabled:

   1. The parent\-child resource relationship is established, and the child resource will be transferred along with the parent resource.

   2. If the associated child resource has the independent transfer prohibition identifier, the child resource cannot be selected for transfer.

4. When it is disabled:

   1. The parent\-child resource relationship is not established, and the child resource will not be transferred along with the parent resource.

   2. Regardless of the independent transfer prohibition identifier, child resources can be selected for transfer.

5. Some parent and child resources do not support the above configuration due to business security issues.


&nbsp;
