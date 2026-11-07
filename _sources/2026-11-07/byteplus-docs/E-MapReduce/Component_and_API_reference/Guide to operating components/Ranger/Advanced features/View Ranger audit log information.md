---
title: "View Ranger audit log information"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/View_Ranger_audit_log_information"
---

Volcano Engine E\-MapReduce (EMR) 1.0 and later versions support viewing audit logs in the /ranger directory of HDFS. You can also view audit logs directly in the Ranger WebUI. After logging in to Ranger Admin, follow these steps.

<span id="_1-access日志"></span>
## **1 Access logs**

Navigation path: Ranger \-\> Audit \-\> Access.

You can view the authentication logs of components.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c16447d217a3c27aaeb80fe8a953f58.png) </span>

Parameter description


|Parameter |Description |
|---|---|
|Policy ID |The ID of the Ranger Policy triggered by the access. |
|Policy Version |The version of the Ranger Policy triggered by the access. |
|Event Time |The time when the access occurred. |
|User |User |
|Service |The name and type of the Ranger Service connected to the accessed service. |
|Resource |The data information accessed. For example, Hive databases, tables, columns, and HDFS paths, and so on.<br><br>Click the icon to view the specific Query information. |
|Access Type |The type of access. |
|Permission |The permission triggered by the access. |
|Result |The result of the access. |
|Access Enforcer |The permission control object triggered by the access. For example, this includes ranger\-acl (Ranger permission control) and hadoop\-acl (HDFS built\-in permission control), and so on.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">HDFS authentication first checks HDFS's built\-in permission control (hadoop\-acl). Only when the built\-in permission control denies access does it check the permissions configured in Ranger (ranger\-acl).</div><br><br><br><div data-tips="true" data-tips-type="tip">You can use this field to determine whether permission control was allowed or denied by hadoop\-acl, or allowed or denied by ranger\-acl.</div><br> |
|Agent Host Name |The hostname of the Ranger Plugin triggered by the access. |
|Client IP |The IP address of the visitor's client. |


<span id="_2-admin-日志"></span>
## **2 Admin logs**

Navigation path: Ranger \-\> Audit \-\> Admin.

You can view Ranger's own operation logs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3198281276c7654f97518df0a225546d.png) </span>

<span id="_3-login-sessions-日志"></span>
## **3 Login Sessions logs**

Navigation path: Ranger \-\> Audit \-\> Login Sessions.

You can view the login activity of Ranger Admin.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3317081442c329cca7b098028fad7c10.png) </span>

<span id="_4-plugins-日志"></span>
## **4 Plugins logs**

Navigation path: Ranger \-\> Audit \-\> Plugins.

You can view the interaction details between Ranger Plugin and Ranger Admin.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_23c9d3710a724b21812618fe8a08bea1.png) </span>

<span id="_5-plugin-status-日志"></span>
## **5 Plugin Status logs**

Navigation path: Ranger \-\> Audit \-\> Plugin Status.

You can view the status information of each Ranger Plugin.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5614ec292a70c8f97489b96c3933cc20.png) </span>

Parameter description


|Parameter |Description |
|---|---|
|Service Name |The name of the Ranger Service connected to the Ranger Plugin. |
|Service Type |The service type of the Ranger Plugin. |
|Host Name |The hostname of the service loaded by the Ranger Plugin. |
|Plugin IP |The IP address of the service loaded by the Ranger Plugin. |
|Last Update |The most recent update time of the policy. |
|Download |The most recent policy download time of the Ranger Plugin. |
|Active |The most recent activity time of the Ranger Plugin. |


<span id="_6-user-sync-日志"></span>
## **6 User Sync logs**

Navigation path: Ranger \-\> Audit \-\> User Sync.

You can view the user synchronization logs of the Ranger UserSync service.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_18f24b71efc062335315b02b4aa1111b.png) </span>

Parameter description


|Parameter |Description |
|---|---|
|Sync Source |The source of synchronized users, including Unix and LDAP/AD. |
|Number Of New |The number of users and user groups added during synchronization. |
|Number Of Modified |The number of users and user groups modified during synchronization. |
|Event Time |The time when synchronization occurs; LDAP/AD synchronizes every minute. |
|Sync Details |Details of user synchronization. |
