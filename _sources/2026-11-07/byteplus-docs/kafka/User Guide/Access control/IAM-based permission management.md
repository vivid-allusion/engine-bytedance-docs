---
title: "IAM-based permission management"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/IAM--permission-management"
---

Identity and Access Management (IAM) is a BytePlus service that offers permission management, allowing you to control how different identities access cloud resources. This topic describes how to manage Message Queue for Kafka resources with IAM.

<span id="bcdbbe10"></span>
## Use scenarios

When enterprise users utilize Message Queue for Kafka, they often choose to create all the necessary resources under a single BytePlus account for centralized or unified management. Different positions in an enterprise require different services and resources. Considering data security and the need for permission isolation, share all resources under a BytePlus account with IAM users. This way, different positions can be granted specific service and resource permissions through the IAM users.

IAM offers fine\-grained access control for resources. You can create IAM users with your BytePlus account and assign permission policies to them to achieve collaborative work or secure access across multiple scenarios. For example, operations personnel can have permission to manage all resources, while marketing personnel can only have permission to view specific resources.

If the BytePlus account already meets your requirements, you do not have to create a separate IAM user for permission management. You can skip this topic without affecting your use of other features in Message Queue for Kafka.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">IAM manages permissions on control plane resources for Message Queue for Kafka, such as permissions on Kafka instances, groups, and topics. To manage data plane resources of Kafka instances, such as specifying permissions for SASL users to send and receive messages, we recommend that you use access control lists (ACLs). For more information, refer to <a href="https://docs.byteplus.com/en/docs/kafka/creating-SASLuser">Creating a SASL user</a>.</div>


<span id="c424dce5"></span>
## Procedure


1. Log on to the IAM console with your BytePlus account.

2. (Optional) Create a custom policy.

   Permissions in IAM include default policies and custom policies. If the default policies do not meet your business requirements, create custom policies in advance. Message Queue for Kafka offers commonly used access policy examples for your reference. For more information, refer to [Access policy templates](https://docs.byteplus.com/en/docs/kafka/access-policy-templates).

3. Create an IAM user and grant permissions.

   IAM users are entity identities in IAM. Each IAM user can correspond to an employee, system, or application within the enterprise. IAM users are not standalone BytePlus accounts and do not own any resources. All resources created by IAM users are billed to the associated BytePlus account.

4. Manage or access resources with IAM users.

   You can log on to the console with IAM users to use features, or call the APIs using AccessKey pairs to use features.


<span id="b43aaa58"></span>
## **Permission policies**

Policies divide permissions based on the API granularity for finer\-grained authorization. This allows precise control over specific actions, resources, and conditions, meeting the enterprise's requirements for minimal permissions in security management. Currently, Message Queue for Kafka supports both default policies and custom policies.

<span id="d5961fb6"></span>
### Default policies


* KafkaFullAccess: grants permissions to perform all operations on all resources in Message Queue for Kafka, such as creating or deleting instances and topics.

* KafkaReadOnlyAccess: only grants read\-only permissions on resources in Message Queue for Kafka, meaning that you cannot create, edit, or delete resources.


<span id="efc5361a"></span>
### **Custom policies**

If the default policies cannot meet actual requirements and you need more granular permission policies, such as allowing an IAM user to view resources of a certain instance or allowing or denying operations on an API, you can create custom policies and authorize specific IAM users.

A BytePlus account has permissions to call all APIs. If an IAM user under the BytePlus account initiates an API request, the IAM user must have the necessary permissions to call the API, or the request fails. Permissions required for an API correspond to authorization items associated with the API. Only users initiating requests and granted the policy corresponding to the authorization item can successfully call the API.

Custom policies are defined with syntax, with key elements including Action and Resource. For more information on the types of resources and related actions that can be authorized in Message Queue for Kafka, refer to [Authorizable resources and actions](https://docs.byteplus.com/en/docs/kafka/authorizable-resources-actions).


* Action: the action that you can perform, such as creating an instance and modifying instance configurations

* Resource: the scope of resources that can be operated on, such as specific instances
