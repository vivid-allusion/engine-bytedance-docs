---
title: "Permission overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Permission_overview"
---

Permission management is an access control capability provided by ArkClaw to implement fine\-grained authorization and security control for resources. Administrators can grant access permissions on resources by department, user group, or individual user to ensure the security and compliance of enterprise data and AI assets.

The permission management module configures the visible scope and executable actions on a per\-resource basis (such as skill libraries, MCP, shared agents). All skills within a skill library automatically follow the same permission rules, ensuring the security of your AI assets and data.

<span id="ZKoK6OSG"></span>
## Related concepts


|Concept |Description |
|---|---|
|Resource type |The resources that the permission management supports, for example, skill libraries, MCP, and shared agents. |
|Skill library (namespace) |The skill library is the management boundary for a set of skills in ArkClaw. |
|Skill |The specific business unit in a skill library. It is the capability that users ultimately download and use. Skills are not independently configured with permissions. The rules of the skill library they belong to apply to them. |
|MCP |AI application assets that enterprises can manage support registration, management, and publishing. Permission management supports global authorization or individual authorization per Tool. |
|Shared agent |Agent applications sourced from "Shared Claw". |
|Permission type |Determines which specific actions users can perform. Available values include **All types** and **Split types**.<br><br><br>* **Skill library**: Can download all skills in the specified skill library.<br><br>* **MCP**: Can invoke applications.<br><br>* **Shared agent**: Can invoke applications. |
|Authorization scope |Determines which users can use the resource. Valid values: **Fully available, Fully unavailable**, and **Partially available**. |
|Authorized entities |The object to which the permissions are granted. Valid values: **User**, **Department**, and **User group**. |
|Dynamic set |When the authorization subject is **All employees**, **Department**, or **User group**, the authorized object is a dynamic set. Members subsequently added to this authorization scope automatically inherit the corresponding permissions, and permissions are automatically revoked when members are removed from the scope.  |


<span id="sSzDbk2T"></span>
## Skills library permission description

Permission rules for the skill library are configured uniformly at the skill library (Namespace) level and cannot be configured for individual skills. After permission rules are configured, newly added skills in the skill library automatically inherit the permission rules of the library.


* The same permission rule applies to all skills in a skill library. You cannot separately configure a different visibility scope or visible subjects for an individual skill in the skill library.

* To enable different skills to have different visibility scopes, you can **split the skill library** to achieve permission isolation and add the skills to different skill libraries.
