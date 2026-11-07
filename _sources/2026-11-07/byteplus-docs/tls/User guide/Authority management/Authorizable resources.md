---
title: "Authorizable resources"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Authorizable_resources"
---

Some TLS API actions support resource\-specific permission management. You can grant permissions on a specified TLS resource to an Identity and Access Management (IAM) user. After the permissions are granted to the IAM user, the IAM user can access the resource. TLS allows you to use IAM to manage the permissions on the following types of Torch Log Service resources.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You must set the parameters such as <code>$region</code> and <code>$account</code> to the actual values corresponding to your BytePlus account.</div>


* <div data-tips="true" data-tips-type="tip">Resources in TLS are organized hierarchically.</div>


   * <div data-tips="true" data-tips-type="tip">Projects are at the root level in the resource hierarchy, and topics, collection rules, scheduled SQL analysis tasks, transformation tasks, ship configurations, dashboards, alarm policies and consumer groups are sub\-resources at the same level.</div>


   * <div data-tips="true" data-tips-type="tip">Host groups, alarm groups, alarm notification content templates, trace instances, and projects are horizontal.</div>




|Resource Type |Permission Description |The Resource Name (TRN) |
|---|---|---|
|Project |The permissions on the specified project or all projects. |* `trn:tls:{$region}:{$accountid}:project/*`<br><br>* `trn:tls:{$region}:{$accountid}:project/{$projectid}` |
|Topic |The permissions on the specified topic or all topics in a specified project. |* `trn:tls:{$region}:{$accountid}:project/{$projectid}/topic/*`<br><br>* `trn:tls:{$region}:{$accountid}:project/{$projectid}/topic/{$topicid}` |
|collection rule |The permissions on the specified collection rule or all collection rules in a specified project. |* `trn:tls:{$region}:{$accountid}:project/{$projectid}/rule/*`<br><br>* `trn:tls:{$region}:{$accountid}:project/{$projectid}/rule/{$ruleid}` |
|Scheduled SQL task |The permissions on the specified scheduled SQL task or scheduled SQL tasks in a specified project. |* `Trn: tls: {$region}: {$accountid}: project/{$projectid}/schedule_sql/*`<br><br>* `trn: tls: {$region}: {$accountid}: project/{$projectid}/schedule_sql/{$schedulesqltaskid}` |
|Dashboard |The permissions on the specified dashboard or all dashboards in a specified project. |* `trn:tls:{$region}:{$accountid}:project/{$projectid}/dashboard/*`<br><br>* `trn:tls:{$region}:{$accountid}:project/{$projectid}/dashboard/{$dashboardid}` |
|Alarm policy |The permissions on the specified alarm policy or all alarm policies in a specified project. |* `trn:tls:{$region}:{$accountid}:project/{$projectid}/alarm/*`<br><br>* `trn:tls:{$region}:{$accountid}:project/{$projectid}/alarm/{$alarmid}` |
|Consumer group |The permissions on the specified consumer group or all consumer groups in a specified project. |* `Trn: tls: {$region}: {$accountid}: project/{$projectid}/consumergroup/*`<br><br>* `trn: tls: {$region}: {$accountid}: project/{$projectid}/consumergroup/{$consumergroupid}` |
|Transformation |The permissions on the specified transformation task or all transformation tasks in a specified project. |* `Trn: tls: {$region}: {$accountid}: project/{$projectid}/etl/*`<br><br>* `trn: tls: {$region}: {$accountid}: project/{$projectid}/etl/{$etltaskid}` |
|Shipping |The permissions on the specified shipping configuration or all shipping configurations in a specified project. |* `Trn: tls: {$region}: {$accountid}: project/{$projectid}/shipper/*`<br><br>* `trn: tls: {$region}: {$accountid}: project/{$projectid}/shipper/{$shipperid}` |
|Host group |The permissions on the specified host group or all host groups. |* `trn:tls:{$region}:{$accountid}:hostgroup/*`<br><br>* `trn:tls:{$region}:{$accountid}:hostgroup/{$hostgroup}` |
|Content template |The permissions on the specified alarm notification content template or all alarm notification<br><br>content templates. |* `Trn: tls: {$region}: {$accountid}: alarm_content_template_type/*`<br><br>* `trn: tls: {$region}: {$accountid}: alarm_content_template_type/{$contenttemplateid}` |
|Alarm notification group |The permissions on the specified notification group or all alarm notification groups. |* `trn:tls:{$region}:{$accountid}:alarmnotifygroup/*`<br><br>* `trn:tls:{$region}:{$accountid}:alarmnotifygroup/{$alarmnotifygroupid}` |
|Trace instance |The permissions on the specified trace instance or all trace instances. |* `trn:tls:{$region}:{$accountid}:traceins/*`<br><br>* `trn:tls:{$region}:{$accountid}:traceins/{$traceinsid}` |


The following table describes the parameters that are used to specify a TRN.


|**Parameter** |**Description** |
|---|---|
|`${region}` |The ID of the Region. |
|`{$accountid}` |The BytePlus account ID. |
|`{$projectid}` |The project ID. |
|`{$topicid}` |The topic ID. |
|`{$ruleid}` |The ID of the collection rule. |
|`{$traceinsid}` |The ID of the trace instance. |
|`{$dashboardid}` |The ID of the dashboard. |
|`{$alarmid}` |The ID of the alarm policy. |
|`{$consumergroupid}` |The ID of the consumer group. |
|`{$etltaskid}` |The ID of the transformation task. |
|`{$shipperid}` |The ID of the shipping configuration. |
|`{$hostgroup}` |The ID of the host group. |
|`{$alarmnotifygroupid}` |The ID of the alarm notification group. |
|`{$contenttemplateid}` |The ID of the notification content template. |
|`{$schedulesqltaskid}` |The ID of the scheduled SQL task. |
