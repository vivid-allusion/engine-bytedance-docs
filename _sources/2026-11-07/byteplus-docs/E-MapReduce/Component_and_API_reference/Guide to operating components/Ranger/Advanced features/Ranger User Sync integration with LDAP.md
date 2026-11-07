---
title: "Ranger User Sync integration with LDAP"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ranger_User_Sync_integration_with_LDAP"
---

By default, Volcano Engine E\-MapReduce (EMR) uses OpenLDAP as the unified user management backend storage, and Ranger UserSync synchronizes from LDAP by default.

<span id="_1-使用前提"></span>
## 1 Prerequisites


1. An EMR cluster with Ranger and OpenLDAP services has already been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. For details on the Ranger UI login interface operations, see [Overview](https://docs.byteplus.com/docs/E-MapReduce/109411) **.** 


<span id="_2-添加用户"></span>
## 2 Add users


1. **Cluster details \-\> User management \-\> Add user**, you can add users in the following two ways:

   * IAM user import: You can use the user management module to import IAM users (including primary accounts and sub\-accounts) into the cluster, enabling these users to use EMR cluster components.

   * Manual user addition: You can use the user management module to create and add custom users to the cluster, enabling these users to use EMR cluster components.

      For details, see [User management](https://docs.byteplus.com/docs/E-MapReduce/105426).

2. After synchronization is complete, the account will be visible in both LDAP and the Ranger WebUI.

   * In LDAP, you can use the following command to check whether the user has been added successfully:

      * Version 1.3.0 and later:

      ```shell
      ldapsearch -b "uid=${uid},ou=user,ou=emr,dc=compute,dc=com" -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
      ```
      

      * Versions prior to 1.3.0:

      ```shell
      ldapsearch -b "uid=${uid},cn=emr,ou=ldap,dc=compute,dc=com" -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
      ```
      

   For details, see [Overview](https://docs.byteplus.com/docs/E-MapReduce/109349).

   * When configuring user permissions in the Ranger WebUI, you can search for the user that was just added.

      For details on how to add permissions, see the permission configuration in each component integration, for example: [Ranger HDFS 集成---新增Policy](https://docs.byteplus.com/docs/E-MapReduce/109415#_3-%E6%96%B0%E5%A2%9Epolicy) **.** 

      After confirming that the user has been added successfully, you can use the account to log in to other components such as Airflow or Hue.
