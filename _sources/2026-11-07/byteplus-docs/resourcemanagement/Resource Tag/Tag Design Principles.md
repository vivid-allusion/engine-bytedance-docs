---
title: "Tag Design Principles"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Design_Principles"
---

Tags are a mechanism for resource classification and management provided by BytePlus. Based on tags, cloud resources with the same characteristics can be classified, queried, and aggregated from different dimensions. This flexible management approach simplifies enterprise resource management.

<span id="principles"></span>
## **Principles**

It is recommended to design a tag management architecture by referring to the following principles during resource tagging:


1. Comprehensive coverage: All core resources should be assigned key\-value pairs during the resource planning phase. This facilitates future tag\-based retrieval and management. For example, if an enterprise has five business teams, the tag key can be department, with five corresponding tag values identifying each team.

2. Limited and simplified tagging: While multiple tags can be attached to a resource, it is recommended to retain only essential tag values and remove redundant ones to prevent misoperations caused by excessive tagging. Additionally, it is advisable to avoid using two or more tag keys for the same attribute. For example, if the key "owner" is used to identify ownership, other synonymous keys such as "belonger" or "possessor" should not be used.

3. Least privilege: Tags can be combined with access control policies to establish a fine\-grained permission management system. To grant tag\-related permissions, the principle of least privilege should be followed. Permissions can be assigned based on various dimensions, including tags attached to resources, tags passed in requests, and tags assigned to request initiators. Employees should only be granted permissions relevant to their roles to mitigate security risks associated with excessive privileges.


<span id="examples"></span>
## **Examples**

The following table provides examples of common business dimensions and their corresponding tag keys and values for reference.


|Business dimension |Tag key |Tag value |
|---|---|---|
|Organizational structure |company, department, organization, and teamgroup |Relevant value |
|Business structure |product, business, module, and service |Relevant value |
|Project\-related |project, schedule, risk, and subtask |Project\-related value |
|Usage |purpose and use |Usage\-related value |
|Role\-based |role and user |System administrator, network administrator, O&M administrator, developer, and tester |
|Personnel type |sponsor, creator, owner, and member |Personnel type\-related value |
