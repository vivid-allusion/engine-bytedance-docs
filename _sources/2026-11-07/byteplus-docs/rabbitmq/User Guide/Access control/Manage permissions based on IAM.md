---
title: "Manage permissions based on IAM"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Manage_permissions_based_on_IAM"
---

Identity and Access Management (IAM) is a permission management service provided by BytePlus. It controls different identity accesses to cloud resources. No payment is required. You only need to pay for the resources in your account. For detailed information about IAM, see [IAM overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-3).

Resources of the message queue for RabbitMQ can be managed with fine\-grained permissions through access control IAM. If you need to assign different access permissions for the RabbitMQ service to different employees in your enterprise to isolate their privileges, you can use BytePlus main account to create additional identities (such as **users**) and grant these identities read\-only or read\-write permissions to enable collaboration or secure access in multiple scenarios.

If the BytePlus main account already meets your needs and you do not need to create independent IAM users for permission management, you may skip this section. It will not affect your use of other functions of the RabbitMQ version of the message queue.

<span id=".55So5oi35LiO6KeS6Imy"></span>
## Users and roles

Users and roles are both identities within IAM.


* Users are divided into main accounts and IAM users. The main account owns all BytePlus resources and has management permissions for all cloud resources. The primary account can create multiple IAM users and authorize them. After authorization, IAM users can perform Actions on Message Queue for RabbitMQ resources based on the granted permissions.

   User groups are collections of users. When a user group associates with a strategy, all users in the group share the corresponding permissions.

* Roles represent another identity in access control. Trusted entities can obtain temporary security credentials by assuming roles and then access cloud resources. It is suitable for scenarios like cross\-service access authorization.


<span id=".5p2D6ZmQ562W55Wl"></span>
## Permission strategy

The strategy splits permissions at the granularity of API interfaces, making authorization more refined. Authorization can be refined to specific operations, resources, and conditions, meeting enterprise security management requirements for minimizing permissions.

Currently, message queue for RabbitMQ supports the following system preset permission policies.


* Full read\-write access (RabbitMQFullAccess): grants all functions and resource operations of message queue for RabbitMQ. For example, it can create instance, delete instance, open extension and close extension.

* Read\-only access (RabbitMQReadOnlyAccess): grants read\-only permission to message queue for RabbitMQ and prohibits actions like create, edit, or delete.
