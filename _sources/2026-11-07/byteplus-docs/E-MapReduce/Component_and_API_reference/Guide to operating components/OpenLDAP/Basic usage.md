---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/openldap_basic_usage"
---

Volcano Engine E\-MapReduce (EMR) uses the OpenLDAP service to manage service system accounts for user clusters, as well as regular accounts created or imported through the console. You can obtain the administrator account and password information for each service from the **Cluster Details** \> **Service List** \> **OpenLDAP** \> **Service Parameters** page in the console.

E\-MapReduce provides the following two methods for managing cluster users:


* **Console operations (recommended)** : Manage users in the cluster from the user management page in the console. This supports importing IAM users, custom user creation, resetting user passwords, deleting users, and group management.

* **Command\-line operations**: Log in to the cluster's primary node and use a series of commands provided by OpenLDAP to manage users in the cluster.


We recommend managing users and user groups in the cluster through the EMR console. Managing cluster users and user groups via the command line will not synchronize changes back to the EMR console.

<span id="_1-控制台操作（推荐）"></span>
## 1 Console operations (recommended)

You can manage cluster users and user groups from the user management page in the console, which is also our recommended approach.

The users displayed in the console are divided into regular users and system users:


* **Regular users**: Users that are imported or created in the console.

* **System users (read\-only)** : Service management accounts that are automatically created during cluster initialization or when adding services. These accounts cannot be edited.


For detailed instructions on managing users through console operations, see [User management](https://docs.byteplus.com/docs/E-MapReduce/105426).

<span id="_2-命令行操作"></span>
## 2 Command\-line operations

<span id="_2-1-用户管理"></span>
### 2.1 User management

To operate OpenLDAP via the command line, you need to provide the password for the admin account. The password can be obtained from the /root/.emr/secret file on the primary node after the cluster is created.

<span id="_2-1-1-创建用户"></span>
#### 2.1.1 **Create user**

Create an ldif file using the following template:


* Version 1.3.0 and later

   ```plaintext
   dn: uid=${uid},ou=user,ou=emr,dc=compute,dc=com
   uid: ${uid}
   cn: ${uid}
   sn: ${uid}
   objectClass: top
   objectClass: person
   objectClass: inetOrgPerson
   objectClass: posixAccount
   userPassword: ${passwd}
   uidNumber: ${uidNumber}
   gidNumber: 500
   homeDirectory: /home/${uid}
   ```
   

* Versions prior to 1.3.0

   ```plain
   dn: uid=${uid},cn=emr,ou=ldap,dc=compute,dc=com
   uid: ${uid}
   cn: ${uid}
   sn: ${uid}
   objectClass: top
   objectClass: person
   objectClass: inetOrgPerson
   objectClass: posixAccount
   userPassword: ${passwd}
   uidNumber: ${uidNumber}
   gidNumber: 500
   homeDirectory: /home/${uid}
   ```
   


Suppose you need to create a user named zhangsan. Replace `${uid}` in the above template with zhangsan, generate the add_user.ldif file, and then run the ldapadd command:

```bash
ldapadd -f add_user.ldif -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The uidNumber must be unique; otherwise, you may encounter permission issues when operating components. User management operations through the EMR console can automatically maintain the uniqueness of uidNumber.</div>


<span id="_2-1-2-查找用户"></span>
#### **2.1.2 Find user**


* Version 1.3.0 and later

   ```bash
   ldapsearch -b "uid=${uid},ou=user,ou=emr,dc=compute,dc=com" -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
   ```
   

* Versions prior to 1.3.0

   ```bash
   ldapsearch -b "uid=${uid},cn=emr,ou=ldap,dc=compute,dc=com" -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
   ```
   


<span id="_2-1-3-删除用户"></span>
#### **2.1.3 Delete user**


* Version 1.3.0 and later

   ```bash
   ldapdelete -x "uid=${uid},ou=user,ou=emr,dc=compute,dc=com" -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
   ```
   

* Versions prior to 1.3.0

   ```bash
   ldapdelete -x "uid=${uid},cn=emr,ou=ldap,dc=compute,dc=com" -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
   ```
   


<span id="_2-1-4-重置密码"></span>
#### **2.1.4 Reset password**


* Version 1.3.0 and later

   ```bash
   ldappasswd -x "uid=${uid},ou=user,ou=emr,dc=compute,dc=com" -s ${new_passwd} -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
   ```
   

* Versions prior to 1.3.0

   ```bash
   ldappasswd -x "uid=${uid},cn=emr,ou=ldap,dc=compute,dc=com" -s ${new_passwd} -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
   ```
   


<span id="_2-2-用户组管理"></span>
### 2.2 User group management

<span id="_2-2-1-创建用户组"></span>
#### 2.2.1 Create user group

Create an LDIF file using the following template:

```plain
dn: cn=${group_name},ou=group,ou=emr,dc=compute,dc=com
cn: ${group_name}
ou: ${group_name}
objectClass: groupOfUniqueNames
uniqueMember: uid=${uid},ou=user,ou=emr,dc=compute,dc=com
```


To create a user group named rd, replace `${group_name}` in the above template with rd, generate the add_group.ldif file, and then run the ldapadd command:

```bash
ldapadd -f add_group.ldif -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">At least one uniqueMember must be specified when creating a user group.</div>


<span id="_2-2-2-查找用户组"></span>
#### 2.2.2 Find user group

```bash
ldapsearch -b "cn=${group_name},ou=group,ou=emr,dc=compute,dc=com" -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
```


<span id="_2-2-3-删除用户组"></span>
#### 2.2.3 Delete user group

```bash
ldapdelete -x "cn=${group_name},ou=group,ou=emr,dc=compute,dc=com" -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
```


<span id="_2-2-4-关联用户"></span>
#### 2.2.4 Associate user

Create an LDIF file using the following template:

```bash
dn: cn=${group_name},ou=group,ou=emr,dc=compute,dc=com
changetype: modify
add: uniqueMember
uniqueMember: uid=${uid},ou=user,ou=emr,dc=compute,dc=com
```


To associate the user zhangsan with the rd user group, replace `${group_name}` in the template with rd, replace `${uid}` with zhangsan, generate the bind_user.ldif file, and then run the ldapmodify command:

```bash
ldapmodify -f bind_user.ldif -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
```


<span id="_2-2-5-解绑用户"></span>
#### 2.2.5 Unbind user

Create an LDIF file using the following template:

```bash
dn: cn=${group_name},ou=group,ou=emr,dc=compute,dc=com
changetype: modify
delete: uniqueMember
uniqueMember: uid=${uid},ou=user,ou=emr,dc=compute,dc=com
```


To unbind the user zhangsan from the rd user group, replace `${group_name}` in the template with rd, replace `${uid}` with zhangsan, generate the unbind_user.ldif file, and then run the ldapmodify command:

```bash
ldapmodify -f unbind_user.ldif -D "cn=admin,dc=compute,dc=com" -w ${openldap_admin_password}
```
