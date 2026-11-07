---
title: "Project management"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Project_management"
---

<span id="introduction"></span>
## Introduction

In the Key Management Service (KMS), each time you create a keyring, new keyring resources are generated. The project management feature is provided by BytePlus to allow you to manage resources of different services or projects by group. You can grant permissions to Identity and Access Management (IAM) roles and users by project, where a project represents a group of resources. This ensures resource isolation and data security.

For more information on projects, refer to [Project management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects).

<span id="note"></span>
## Note


* Keyrings are the only KMS resources that can be managed by the project management feature.

* As a child resource of a keyring, a single key cannot be managed through project management.

* One resource can belong to only one project.

* When you create a new resource, it is added to the default project if you do not specify a project for it.

* After a resource is added to a project, the resource can be used only by users with permissions for the project.

* The association between resources does not change after the resources are added to projects.

* If you need to associate resources from multiple projects, you must have permissions for all the projects of the resources to associate. For example, if you need to associate Keyring 1 in Project A with Keyring 2 in Project B, you must have permissions for both Projects A and B. For more information on permission authorization, refer to [Editing a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project).

* When you use a sub\-account to create and manage resources, make sure that the sub\-account is granted the required permissions by the main account.


<span id="viewing-project-and-resource-information"></span>
## Viewing project and resource information

<span id="searching-for-resources-by-project"></span>
### Searching for resources by project


1. Log on to the [KMS console](https://console.byteplus.com/kms/).

2. In the top navigation bar, select a region and select a project as required.

   1. To view all resources under the current account, select **All resources**.

   2. Note the following:

      * After you log on with a main account or a sub\-account, all resources under the account are displayed by default.

      * If the sub\-account is not granted global permissions, the resources displayed when you select **All resources** are not all the resources under the account. To view all resources, contact the main account to obtain permissions, or select different projects to view resources by project.

   3. Select a specific project to view all resources associated with the project.

   4. Click **Manage projects** to go to the project list page to manage the projects.
