---
title: "Overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/openldap_overview"
---

Volcano Engine E\-MapReduce (EMR) uses the OpenLDAP service to manage users and user groups within the cluster. Other services in the cluster use OpenLDAP for access authentication by default.

<span id="_1-前提条件"></span>
## 1 Prerequisites

An EMR cluster has been created. For cluster types that support user management (these clusters include OpenLDAP as a required component), the OpenLDAP service is installed by default when the cluster is created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

<span id="_2-部署拓扑"></span>
## 2 Deployment topology


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation bar of the console, click **Cluster Management** \> **Cluster List** \> **Cluster Name** to enter the details page for the specific cluster.

3. On the cluster details page, click **Service List** \> **OpenLDAP** \> **Deployment Topology** tab to view the specific deployment node information for OpenLDAP.


In non\-HA mode, OpenLDAP is deployed on one primary node. If HA mode is enabled when creating the cluster, OpenLDAP will be deployed on two primary nodes and use [Mirror mode](https://www.openldap.org/doc/admin25/replication.html) for mutual hot standby.

<span id="_3-dn-格式变更说明"></span>
## 3 DN format change note


* Before version 1.3.0, the user DN format for EMR clusters was:

   ```plain
   uid=${user_name},cn=emr,ou=ldap,dc=compute,dc=com
   ```
   

* Starting from version 1.3.0, EMR clusters introduced support for user groups and optimized the user DN format. The updated format is as follows:

   * User DN format:

   ```sql
   uid=${user_name},ou=user,ou=emr,dc=compute,dc=com
   ```
   

   * User group DN format:

   ```sql
   cn=${group_name},ou=group,ou=emr,dc=compute,dc=com
   ```
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When initializing the cluster, the OpenLDAP service includes a system user group with the DN "cn=admin,ou=group,ou=emr,dc=compute,dc=com" for managing system accounts. Do not delete this user group arbitrarily, as this will affect the normal operation of the user management module.</div>
