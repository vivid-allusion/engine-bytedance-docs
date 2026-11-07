---
title: "Overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-Overview"
---

You can use the Application Load Balancer (ALB) service as an Identity and Access Management (IAM) user.


* After you register on BytePlus, the system automatically creates a root account for you. When your enterprise purchases multiple services on BytePlus using a root account, such as Elastic Compute Service (ECS), ALB, and elastic IP address (EIP), the root account has full access control permissions for these services. Additionally, the root account is the billing entity.

* If an employee in your enterprise requires the EIP service but not the ALB service, you can use the identity management capability of the IAM feature to create an IAM user for the employee and grant the IAM user only the necessary permissions for EIP to complete their work.

* IAM is a permission management system from BytePlus that manages access to cloud services for different identities.

* New IAM users can log in to BytePlus with their own usernames and passwords. You can create multiple IAM users and grant them different permissions to manage cloud services, improving management efficiency and reducing the risk of information leakage. 


<span id=".5Z-65pys5qaC5b-1"></span>
## **Terms**


|Term |Description |
|---|---|
|Root account |Upon your registration on the BytePlus website, you own a root account. The root account has, by default, permissions to call OpenAPIs and manage all services in the console. It can perform actions such as purchasing, renewing, unsubscribing, and upgrading resources, and it has access to all associated orders and bills. |
|IAM user |An IAM user is an identity created and granted appropriate permissions by a root account or an authorized user. It can log in to the console or use access key to call APIs to access cloud services.  |
|User group |A collection of IAM users. The same IAM user can belong to multiple user groups. The attached policies of a user group define its permissions. Once a policy is attached to a user group, all users in that group inherit the corresponding permissions.  |
|Role |A role is another type of identity that cannot directly access cloud services. It must first establish a trust relationship that authorizes other identities to assume the role. A trusted identity assumes a role to get temporary credentials for accessing cloud services.  Supported types of identities trusted by a role:<br><br><br>* User: It can be a real user or a service. After being trusted by a role, a user can use temporary credentials to access cloud service resources securely.<br><br>* Account: A role can configure trust relationships for the current account or for another account.<br><br>* Service: This refers to BytePlus's cloud services. After a role grants trust to a service, the service can act as an account to access other cloud resources.<br><br>* Identity provider (IdP): This refers to the customer's own identity service. Customers can establish a trust relationship between their own IdP and BytePlus IAM via federated login, enabling single sign\-on (SSO) to the BytePlus console. |
|Policy |A policy is a formal statement that defines permissions. IAM supports identity\-based policies and resource\-based policies. Whether users, user groups, or roles, permissions are granted by attaching policies.<br><br><br>* Identity\-based policies: Policies attached to an identity, granting that identity access to a cloud resource.<br><br>* Resource\-based policies: Policies attached to a resource, specifying which identities can access the resource and how. Note: An IAM role is both an identity and a resource. In the identity context, a role requires an attached permission policy to define its access permissions (related to the temporary credentials generated upon assuming the role). In the resource context, a role requires an attached trust policy to define which identities can access it (i.e., who can assume the role).  |
|Project |A project is a collection of resources. When creating a cloud resource, you can select a specific project for it. Additionally, you can query, add, or remove resources within a project on the Resource Project console.  |
