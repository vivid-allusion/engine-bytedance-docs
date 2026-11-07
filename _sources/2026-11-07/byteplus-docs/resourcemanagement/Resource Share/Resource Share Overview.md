---
title: "Resource Share Overview"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Resource_Share_Overview"
---

Resource Share (RS) enables BytePlus users to securely share resources across accounts. In a multi\-account scenario, users can share resources under their accounts with designated users and restrict the operation permissions on the shared resources. After the sharing is completed, the designated users can directly use the shared resources without the need to create resources repeatedly.

<span id="benefits"></span>
## Benefits


1. **Reduce management complexity**: Creating resource instances in one account and sharing them with other accounts avoids duplicate creation and configuration of resources under each account and reduces the complexity of resource management. Resource owners can centrally manage the sharing configuration for resource instances by using RS, which improves operational efficiency and ensures the consistency of resource sharing configuration.

2. **Enhance management security**: RS has built\-in sharing policies for different resource types to ensure that shared resources meet business requirements while restricting users from accessing unauthorized resources, thus enhancing the security of resource management. Enterprises can conduct unified O&M control of shared resources, making it convenient for enterprises to centrally configure security policies and audit trails.

3. **Enhance the sharing experience**: Resources are provided based on the same sharing mechanism, so users do not need to adapt to the differentiated sharing operations of different cloud resources. After sharing with enterprise organization is enabled, you can share resources with the entire organization or its OUs, and RS can automatically grant or revoke the shared resource access permissions of the corresponding account based on the account changes under the organization or its OUs.


<span id="shareable-resources"></span>
## Shareable resources


|**Resource Type** |**Description** |
|---|---|
|ModelArk \- Dataset |All users can initiate sharing and accept share invitations for datasets. |
|ModelArk \- Model card |Active sharing is available to only some users, but all users can accept share invitations. To use the feature, go to Work order center to submit a work order. |
|ModelArk \- Custom model |Active sharing is available to only some users, but all users can accept share invitations. To use the feature, go to Work order center to submit a work order. |
|StorageEbs \- Snapshot |Active sharing is available to only some users, but all users can accept share invitations. To use the feature, go to Work order center to submit a work order. |
|VPC \- Subnet |Active sharing is available to only some users, but all users can accept share invitations. To use the feature, go to Work order center to submit a work order. |


<span id="concepts"></span>
## Concepts


|**Term** |**Description** |
|---|---|
|Shared unit |A shared unit is an instance of resource sharing. The shared unit itself is also a cloud resource that belongs to RS. Shared units are regional, and you need to switch to the relevant region when managing shared units. A shared unit can be associated with only resources in the same region. The process of creating a share involves configuring basic information and associating resources, associating sharing permissions, associating shared users, and confirming and submitting. |
|Resource owner |A resource owner is the initiator of a resource share, who shares a resource with designated accounts or organizations and is also the owner of the shared resource, which manages resource shares in a centralized manner. |
|Shared user |A shared user is the beneficiary of a resource share, who has specific permissions to operate and use a shared resource, and can actively choose to accept or reject share invitations.<br><br>> If a share is initiated within an enterprise organization, the member accounts in the organization and its OUs accept the share invitation by default. The shared users cannot opt out of the share themselves. They need to contact the resource owner to cancel the share. |
|Shared resource |A shared resource is a resource instance of a cloud service type. A shared unit can contain multiple types of resource instances in the same region. |
|Sharing policy |Each type of shareable resource must be associated with a sharing policy of the same type. A policy strictly restricts the actions that a shared user can perform on a shared resource. |


<span id="sharing-methods"></span>
## Sharing methods


|**Sharing Method** |**Description** |
|---|---|
|Allow sharing with any account |The owner of a resource can share the resource with any main account, or with the entire organization, departments, or member accounts if the resource owner is in the organization.<br><br><br>> * Accounts that have not joined the enterprise organization can share resources with designated accounts.<br><br>> * The administrator account of an enterprise organization can share resources with designated accounts outside the enterprise organization.<br><br>> * The administrator account of an enterprise organization can share resources with the organization and its OUs or member accounts. |
|Allow sharing with organization |To use this method, the owner of a resource must be an enterprise organization administrator. The resource can only be shared with the organization and its OUs or member accounts. At present, VPC \- Subnet is only supported for sharing with enterprise organization。 |
