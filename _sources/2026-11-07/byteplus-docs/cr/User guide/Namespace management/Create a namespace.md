---
title: "Create a namespace"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/create-a-namespace"
---

A namespace serves to group related image repositories and Helm Charts for management. It does not directly store container images or Helm Charts. Within a company, a namespace typically maps to a product project or a business department.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Created instance. For instructions, see [Create Standard instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

* (Optional) Project authorization has been completed. For detailed actions, see [Add project authorization ](https://docs.byteplus.com/en/docs/cr/grant-project-permissions).

* Only the root user or IAM users granted the CRFullAccess policy permission (full read\-write access to CR) can create namespaces. For instructions on granting IAM users full read and write permissions to CR, see [Authorize IAM user ](https://docs.byteplus.com/en/docs/cr/authorize-iam-users).


<span id=".5Yib5bu65ZG95ZCN56m66Ze0"></span>
## Create a namespace


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar of the instance page, click **namespace**.

3. On the **Namespaces** page, click **Create namespace**.

4. Configure the namespace parameters.

   
   |Parameter |Description |
   |---|---|
   |Name |Customize the name of the namespace. The namespace name must be unique within the same instance. |
   |Associated project |The associated target project. After association, members of that project will inherit corresponding permissions for the CR services based on project authorization. For operating instructions, see [Project management ](https://docs.byteplus.com/en/docs/organization/OrganizationSetup). |
   |Default repository type |Set the default public or private type of artifact repositories under this namespace.<br><br><br>* **Private**: A private OCI artifact repository type that requires entering an access key before access.<br><br>* **Public**: A public OCI artifact repository type that does not require an access key and supports direct access. |
   |Maximum storage capacity |Select whether to set the maximum storage capacity for the namespace.<br><br><br>* **Unlimited**: Do not set an upper limit for the storage capacity of the namespace.<br><br>* **Limited**: Set an upper limit for the storage capacity of the namespace. Once the limit is exceeded, pushing OCI artifacts to this namespace is not supported. |
   

5. Click **Confirm** to complete the creation of the namespace.
