---
title: "Best Practices"
product: "BytePlus Organization"
product_code: "organization"
source: "https://docs.byteplus.com/en/docs/organization/BestPractices"
---

<span id="mapping-enterprise-business-architecture-to-the-cloud"></span>
## Mapping Enterprise Business Architecture to the Cloud

When migrating an enterprise to the cloud, the first step is to map its business entities to corresponding BytePlus identity objects. The recommended mapping structure depends on the architectural design. The following table outlines the characteristics of different BytePlus identity objects and their recommended mappings for enterprise\-wide and R&D project\-based structures.


| |BytePlus identity object |Enterprise\-wide architecture mapping |R&D project\-based architecture mapping |
|---|---|---|---|
|Master Account |The administrator of an Organization. A Master Account has the highest read/write permissions within the account group. This account can access and manage the cloud resources and data under Member Accounts. |Headquarters |Cost management center/IT management center |
|Organizational Unit |A node within the Organization that represents the hierarchical structure of an Organization. Accounts and other Organizational Units can be attached to this node. Organizational Units enable efficient account management. For example, all accounts related to Subsidiary A can be attached to Organizational Unit A and the Control Policy of "Deny Access to Cloud Enterprise Network" can be associated with Organizational Unit A. This enables centralized access management for all Member Accounts within Subsidiary A. |/ |R&D departments/Specialized R&D teams |
|Member Account |A member within the Organization, whose cloud resources and data are managed by and accessible to the administrator. Each member account has its own separate resources and bills. Therefore, it is suitable for IT projects or business divisions that do not share resources or require strict confidentiality. |Subsidiaries |Independent R&D projects within an Organizational Unit |
|IAM User Group |A collection of users in the access control system of an account. An IAM User Group represents a group of individuals whose permissions are assigned and managed in a centralized manner and can only access and manage resources within the account. |Business teams |R&D teams |
|IAM User |A user within the access control system of an account. An IAM User represents an individual or application who can be assigned specific permissions to access and manage resources within the account. |Employees |R&D personnel |
|IAM Role |A role within the access control system of an account. The role defines a set of permissions. |Functional roles such as IT O&M administrator |Designers, front\-end and back\-end developers, testers, and O&M personnel |
