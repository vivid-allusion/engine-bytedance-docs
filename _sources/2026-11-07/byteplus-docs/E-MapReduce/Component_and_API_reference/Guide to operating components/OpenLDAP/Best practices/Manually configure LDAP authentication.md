---
title: "Manually configure LDAP authentication"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Manually_configure_LDAP_authentication"
---

The EMR console provides the OpenLDAP service to manage cluster users and user groups. To integrate with a self\-hosted LDAP service, manual configuration is required to enable LDAP authentication for each service.

<span id="hive配置"></span>
## Hive configuration

You need to manually configure the LDAP authentication information for HiveServer2. On the **service parameter configuration** page of the Hive service in the EMR console, modify the following configuration items.


|**Configuration item** |**Reference value** |**Note** |
|---|---|---|
|hive.server2.authentication.ldap.url |ldap://{ldap_hostname}:{port}<br><br>For example: ldap://master\-1\-1:389 |Used to specify the URL for connecting to the LDAP service. Configuration must be performed according to actual requirements.<br><br><br>* {ldap_hostname}: The hostname or IP address of the LDAP service.<br><br>* {port}: The port of the LDAP service. The LDAP service port for the EMR cluster is 389. For a self\-hosted LDAP service, enter the actual port. |
|hive.server2.authentication.ldap.baseDN |ou=user,ou=emr,dc=compute,dc=com |Used to specify the Base DN where users are located in the LDAP service. The LDAP for the EMR cluster is `ou=user,ou=emr,dc=compute,dc=com`. For a self\-hosted LDAP service, enter the actual value. |


<span id="hue配置"></span>
## Hue configuration


|**Configuration item** |**Reference value** |**Note** |
|---|---|---|
|usersync.ldap.url |ldap://{ldap_hostname}:{port}<br><br>For example: ldap://master\-1\-1:389. |Update LDAP connection information for Hue login |
|usersync.ldap.username.pattern |"uid=,ou=user,ou=emr,dc=compute,dc=com" ||
|usersync.ldap.force.username.lowercase |False ||
|usersync.ldap.bind.dn |"cn=admin,dc=compute,dc=com" |Disable admin login by leaving this parameter empty |
|usersync.ldap.bind.password |<br>---<br><br> ||
|usersync.ldap.base.dn |"ou=emr,dc=compute,dc=com" |Update LDAP connection information for other services (such as Hive connection) |
|usersync.ldap.username.pattern |"uid=,ou=user,ou=emr,dc=compute,dc=com" ||
|auth_username |admin |Update Hive and Spark authentication information<br><br>By default, there are account credentials for connecting to Hive and Spark. These must be changed to an account and password from IDC; otherwise, authentication errors will occur when using Hive and Spark. |
|auth_password |<br>---<br><br> ||


<span id="spark配置"></span>
## Spark configuration


|**Configuration item** |**Reference value** |**Note** |
|---|---|---|
|hive.server2.authentication.ldap.baseDN |ou=user,ou=emr,dc=compute,dc=com |Used to specify the Base DN where users are located in the LDAP service. The LDAP for the EMR cluster is `ou=user,ou=emr,dc=compute,dc=com`. For a self\-hosted LDAP service, enter the actual value. |
|hive.server2.authentication.ldap.url |ldap://{ldap_hostname}:{port}<br><br>For example: ldap://master\-1\-1:389. |Used to specify the URL for connecting to the LDAP service. Configuration must be performed according to actual requirements.<br><br><br>* {ldap_hostname}: The hostname or IP address of the LDAP service.<br><br>* {port}: The port of the LDAP service. The LDAP service port for the EMR cluster is 389. For a self\-hosted LDAP service, enter the actual port. |
