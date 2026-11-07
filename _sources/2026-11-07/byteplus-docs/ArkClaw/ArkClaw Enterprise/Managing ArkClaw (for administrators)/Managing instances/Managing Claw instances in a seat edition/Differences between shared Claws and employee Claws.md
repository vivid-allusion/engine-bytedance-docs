---
title: "Differences between shared Claws and employee Claws"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Differences_between_shared_and_employee_Claw_instances"
---

Shared Claws and employee Claws are suitable for different permission and asset accumulation scenarios. This topic compares their differences in **ownership, permission model, knowledge management, and quota attribution**. It also provides the corresponding access points for creating, managing, and deleting them to help you understand Claw instance types.


<card mode="container" href="" iconSet="1" horizontal="1" iconSize="" icon="" img="" >

Shared Claw

Shared Claw instances are accessible to team members based on permissions. They apply to collaborative workflows that require unified agent configurations, shared knowledge bases, and standardized execution environments.

</card>




<card mode="container" href="" iconSet="1" horizontal="1" iconSize="" icon="" img="" >

Employee Claw

Employee Claw instances are mainly used by individual employees. They are configured by and belong to individual employees.

</card>



<span id="z8SiSXIc"></span>
## Functionality differences


|Dimension |Shared Claw  |Employee Claw |
|---|---|---|
|**Positioning and ownership** |||
|Functional positioning |A Claw instance that can be reused in the organization. It contains shared knowledge and capabilities and can be used by multiple users with permissions. |A Claw instance used by the employee. The instance hosts personal agent configurations, knowledge, and task execution environments. |
|Ownership |It is managed at the organization level and maintained by enterprise administrators and shared Claw administrators. |It is owned by the employee by default. |
|**Permission model and availability scope** |||
|Permission structure | Permissions are divided into two roles: administrators (designated by enterprise administrators) and regular users.<br><br><br>* Administrators: They can modify configurations such as switching models and editing the soul settings. This role is suitable for team administrators and platform owners.<br><br>* Users: They can only initiate tasks and view results within the authorization scope. This role is suitable for business users. |It is owned by the employee and does not require designating additional administrators. |
|Visibility scope |Only administrators and employees with granted permissions can view shared Claw instances under the “Shared Claw” category. |It is typically visible and available only to the employee in the "My Claw" list. |
|**Knowledge management** |||
|Knowledge ownership |A shared Claw serves as the carrier for centralized accumulation. It is an organizational asset and can be reused by multiple authorized members. |The knowledge belongs to the employee's Claw instance. |
|Management method |Maintained by administrators centrally. Continuous updates and management are supported. |Maintained by the employee. |
|**Feature availability scope limit** |||
|Openness |Capabilities are limited by default to reduce security risks caused by high\-risk operations. |Its capabilities are relatively complete, and flexible configuration is supported. |
|**Quota and resource ownership** |||
|Quota ownership |Consumes the seat edition quota of the ArkClaw space. |Consumes the per\-edition seat quota allocated to the employee. |


<span id="uXmnuBDo"></span>
## Operation differences


|Configuration |Shared Claw  |Employee Claw |
|---|---|---|
|**Creation** |**Enterprise administrators** and **employees** can create shared Claw instances.<br><br><br>* **Enterprise administrators**: When an enterprise administrator registers an Agent application of the "shared Claw" type, the system automatically creates the corresponding shared Claw instance. For details, see [Registering Agent applications](https://docs.byteplus.com/en/docs/ArkClaw/Application_management?lang=en#Mxxy9IhZ).<br><br>* **Enterprise employees**: Enterprise employees can directly create a shared Claw instance. For details, see [Creating Claw instances](https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw_). |* **Employees** create employee Claw instances in the ArkClaw console. For details, see [Applying for Claw instances](https://docs.byteplus.com/en/docs/ArkClaw/Applying_for_ArkClaw_instances_?lang=en). |
|**Management** |**Enterprise administrators** can manage  shared Claw instances in the Shared Claw list. For details, see [Managing Claw instances](https://docs.byteplus.com/en/docs/ArkClaw/Managing_Claw_instances_in_a_seat_edition?lang=en).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip</div><br><br><br><div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Operations such as enabling/disabling, backup/restore, and auto\-healing are performed in the same way for both shared and employee Claw instances. The difference is that shared Claw instances support <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configure_shared_Claw_instance_administrators?lang=en">configuring instance administrators</a>.</div><br> |* After an employee Claw instance is created, **enterprise administrators** can manage it in the employee Claw list. For details, see [Managing Claw instances](https://docs.byteplus.com/en/docs/ArkClaw/Managing_Claw_instances_in_a_seat_edition?lang=en). |
|**Deletion** |* You cannot directly delete shared Claw instances from the shared Claw instance list.<br><br>* To delete a shared Claw instance, the **enterprise administrator** must unregister the agent application where the shared Claw instance resides in the Application Center. For details, see [Unregistering applications](https://docs.byteplus.com/en/docs/ArkClaw/Managing_applications?lang=en#cUBogHKm). |* When an employee Claw instance is no longer in use, the **enterprise administrator** can directly delete the employee Claw instance from the employee Claw instance list. For details, see [Deleting Claw instances](https://docs.byteplus.com/en/docs/ArkClaw/Deleting_Claw_instances). |


<span id="YkIJGNCF"></span>
##
