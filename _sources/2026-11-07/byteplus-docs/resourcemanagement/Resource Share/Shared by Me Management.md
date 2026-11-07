---
title: "Shared by Me Management"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Shared_by_Me_Management"
---

Resource owners can share resources with designated users and effectively restrict the operation permissions on the shared resources. The shared by me feature supports shared unit creation, shared unit viewing, shared unit modification, shared unit deletion, shared resource viewing, and shared user viewing.

<span id="creating-shared-unit"></span>
## Creating shared unit


1. Log in to Resource management and go to [Resource sharing > Shared by me](https://console.byteplus.com/resourcemanager/region:resource-manager+ap-southeast-1/resource_share/owned) in the left navigation bar.

2. Select the region with the relevant resources in the top menu bar.

3. Click Create shared unit to enter the creation process.

4. Step 1: Configure basic information and associate resources.

   1. Enter the shared unit name. The name can contain up to 50 characters, including letters, digits, Chinese characters, periods (.), underscores (_), and hyphens (\-).

   2. Specify the resource type and select the resource to be shared.

> Resources of different types in the same region can be selected. If no information about the resource that can be shared is displayed in the resource list, check whether you have the query permission on the resource and whether the target region is selected in the top menu bar.


   3. Click View selected resource in the lower left corner to view all types of resources that have been selected for sharing. These resources can be removed.

   4. Click Next.

5. Step 2: Associate sharing permissions.

   1. Select the permissions that allow shared users to perform operations on the shared resources.

> The system will automatically associate the predefined policy library based on the resource type, and you can click to view the policy details.


   2. Click Next.

6. Step 3: Associate shared users.

   1. Select the resource user scope. Two options are provided: Allow sharing with any account and Allow sharing with organization.

>    * Allow sharing with any account: Resource owners can share resources with any main account, and if the resource owner is in an enterprise organization, the resource can be shared within the entire organization, including the departments and member accounts.

>    * Allow sharing with organization: Resource owners must belong to an enterprise organization, and the resource can only be shared with the organization and its OUs or member accounts. This option is available only to enterprise administrators.

   2. You can add a shared user by either selecting from the enterprise organization or selecting the user type and specifying the user ID.

>    * Select from organization: Only enterprise administrators can select the organization, OU, and member accounts from the organization tree directory to add shared users.

>    * Select user type and specify user ID: Shared users can be added by specifying the account ID, organization ID, and organization OU ID.

   3. Click Next.

7. Step 4: Confirm and submit.

   1. Confirm the entered information again, including the shared unit name, resources and associated permissions, and shared users.

   2. Click Confirm.

8. Go to Shared by me and click Shared unit. If the newly created shared unit is in the Enabled state, the shared unit is created successfully.


<span id="viewing-shared-unit"></span>
## Viewing shared unit


1. Log in to Resource management and go to [Resource sharing > Shared by me](https://console.byteplus.com/resourcemanager/region:resource-manager+ap-southeast-1/resource_share/owned) in the left navigation bar.

2. Select the region with the relevant shared unit in the top menu bar.

3. Click Shared unit and search for shared units by shared unit ID or name.

4. Click Details in the Actions column of a specified shared unit.

5. View the basic information of the shared unit, including shared unit ID, shared unit name, status, creation time, and user scope.

> A shared unit has two states, namely, enabled and deleted. A shared unit becomes enabled after it is created. A deleted shared unit is still visible but can no longer be edited, and it becomes invisible after 48 hours.


6. View the associated resources of the shared unit, including basic information about shared resources, associated policies, and association status.

> An associated resource has two states, namely, associated and disassociated. After sharing, all the resources in the shared unit are associated. If some resources in the shared unit are deleted, they are disassociated and become invisible after 48 hours.


7. View the shared users of the shared unit, including shared user ID, type, and association status.

> A shared user has two states, namely, associated and disassociated. After sharing, all the resources in the shared unit are associated. After the sharing invitation is accepted, the shared user is associated. After disassociation, the shared user is disassociated and becomes invisible after 48 hours.


<span id="viewing-shared-resource"></span>
## Viewing shared resource


1. Log in to Resource management and go to [Resource sharing > Shared by me](https://console.byteplus.com/resourcemanager/region:resource-manager+ap-southeast-1/resource_share/owned) in the left navigation bar.

2. Click Shared resource and search for shared resources by shared resource ID.

3. View the basic information of the shared resource, including resource ID, resource type, shared unit, and shared user.

4. You can click the resource to go to the relevant product console.


<span id="viewing-shared-user"></span>
## Viewing shared user


1. Log in to Resource management and go to [Resource sharing > Shared by me](https://console.byteplus.com/resourcemanager/region:resource-manager+ap-southeast-1/resource_share/owned) in the left navigation bar.

2. Click Shared user and search for shared users by main account ID, department ID, or organization ID.

3. View the basic information of the shared user, including user ID, user type, shared unit, and shared resource.


<span id="editing-shared-unit"></span>
## Editing shared unit


1. Log in to Resource management and go to [Resource sharing > Shared by me](https://console.byteplus.com/resourcemanager/region:resource-manager+ap-southeast-1/resource_share/owned) in the left navigation bar.

2. Click Shared unit and click Details in the Actions column of a specified shared unit.

3. Click Edit shared unit in the upper right corner.

4. On the Edit shared unit page, you can modify the shared unit name, add or remove shared resources, and add or remove shared users.


<span id="deleting-shared-unit"></span>
## Deleting shared unit


1. Log in to Resource management and go to [Resource sharing > Shared by me](https://console.byteplus.com/resourcemanager/region:resource-manager+ap-southeast-1/resource_share/owned) in the left navigation bar.

2. Click Shared unit and click Details in the Actions column of a specified shared unit.

3. Click Delete shared unit in the upper right corner. The shared resources will no longer be available to the associated shared user after deletion.
