---
title: "Roles and permissions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_roles_and_permissions"
---

<span id="adb5b4b9"></span>
# Sub\-account authorization guide

The tenant primary account is granted permissions equivalent to EMRFullAccess by default. By default, sub\-accounts are not assigned any roles and do not have EMR product permissions. Therefore, after creating an IAM sub\-account, you must authorize the sub\-account based on actual requirements. Recommended authorization operations are as follows. For detailed IAM sub\-account authorization procedure, see below.


1. You can create the required permission scope for each business personnel role on the "Permission policy" page in the Access Control (IAM) console.

   * EMR provides preset permission policies for common business roles (EMRFullAccess, EMRDeveloperAccess, EMRReadOnlyAccess). You can authorize sub\-accounts directly using these preset permission policies based on actual business requirements. The permission scope supported by preset permission policies can be found in the following [Preset permission policies](https://docs.byteplus.com/docs/E-MapReduce/105450#%E8%A7%92%E8%89%B2)section.

   * You can also create Customer managed permission policies as needed. When creating a Customer managed permission policy, select the service "E\-MapReduce" and use the graphical interface to configure the EMR operation permissions for the current policy. Alternatively, you can use the JSON editor to set detailed EMR permission scopes in JSON format.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27da61b004e24e28a008ed30b7e5440d~tplv-goo7wpa0wc-image.image) </span>

2. After the permission policy is created, you can directly grant the corresponding permission policy to the sub\-account. You can also create an IAM role, grant the permission policy to the role, and then simply add the newly created IAM sub\-account to the corresponding role. The IAM sub\-account will then have the permissions of that role. For operation details, see: [IAM role management](https://www.volcengine.com/docs/6257/64979).


<span id="7dc6b529"></span>
# Note on preset permission policies

<span id="角色"></span>
## **Preset permission policies**

EMR provides the following preset permission policies for common business roles on the Access Control console page. You can authorize sub\-accounts directly using these preset permission policies based on actual business requirements, or create Customer managed permission policies as needed.


|Preset permission policies |Scope of functionality |Data permissions |
|---|---|---|
|EMRFullAccess |Grants users full permissions for all EMR operations. |All |
|EMRDeveloperAccess |Grants users all permissions except for those related to orders and payment, specifically creation, release, and scaling. |All |
|EMRReadOnlyAccess |Allows users read\-only permissions for EMR console operations. |All |


<span id="权限"></span>
## **Note on permission scope**


|Function |Function description |EMRFullAccess |EMRDeveloperAccess |EMRReadOnlyAccess |
|---|---|---|---|---|
|Overview page |View |✅ |✅ |✅ |
|Cluster list |View list |✅ |✅ |✅ |
| |Restart |✅ |✅ |❌ |
| |Custom cluster creation |✅ |❌ |❌ |
| |Quick cluster creation |✅ |❌ |❌ |
| |Release |✅ |❌ |❌ |
|Historical cluster list |View list |✅ |✅ |✅ |
|View basic cluster information |View cluster information |✅ |✅ |✅ |
| |Cluster operation logs |✅ |✅ |✅ |
|Cluster service management |View service list |✅ |✅ |✅ |
| |Add service |✅ |✅ |❌ |
| |Service operations (start, stop, restart) |✅ |✅ |❌ |
| |Component deployment topology list |✅ |✅ |✅ |
| |Component operations (start, stop, restart) |✅ |✅ |❌ |
| |Service configuration (Save, deploy, and restart) |✅ |✅ |❌ |
|Host management |View host list |✅ |✅ |✅ |
| |Manual scaling |✅ |❌ |❌ |
|User management |View IAM user import list |✅ |✅ |✅ |
| |Import user |✅ |✅ |❌ |
| |Remove user |✅ |✅ |❌ |
| |Reset password |✅ |✅ |❌ |
|Alert management |View alert rule list |✅ |✅ |✅ |
| |Create alert rule |✅ |✅ |❌ |
| |Edit alert rule |✅ |✅ |❌ |
| |Delete alert rule |✅ |✅ |❌ |
|Machine group management |View machine group list |✅ |✅ |✅ |
| |Create machine group |✅ |✅ |❌ |
| |Delete machine group |✅ |✅ |❌ |
|Monitoring and metrics |View alert rule list |✅ |✅ |✅ |
| |Obtain monitoring metric items |✅ |✅ |✅ |
| |Query monitoring metric data |✅ |✅ |✅ |
| |Export monitoring metric data |✅ |✅ |❌ |
| |Obtain cluster monitoring summary information |✅ |✅ |✅ |
| |Obtain detailed cluster monitoring information |✅ |✅ |✅ |
| |Obtain log file information |✅ |✅ |✅ |
| |Log search |✅ |✅ |✅ |
| |Log context query |✅ |✅ |✅ |
