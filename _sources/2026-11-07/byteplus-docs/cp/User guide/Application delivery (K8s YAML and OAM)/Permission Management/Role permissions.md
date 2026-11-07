---
title: "Role permissions"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Role_permissions"
---

Application delivery members are divided into five roles: administrator, developer, tester, operations, and read\-only. Each role has different default permissions. Assigning different roles to members within an application enables fine\-grained permission control over the application's resources, configurations, and other resources. This article introduces the permissions available to each role in each functional module.


| |Administrators |Development |Test |Operations and maintenance |Read\-only |
|---|---|---|---|---|---|
|**environment** |Read/write access<br><br>Has full read and write permissions for all environment types. |Partial read/write<br><br>Has full read and write permissions for the development environment type. |Partial read\-write<br><br>Have full read and write access to the test environment type. |Full read/write<br><br>Has full read and write permissions for all environment types. |Read\-only |
|**Application orchestration** |Full read/write<br><br>You can modify application orchestration content. |Read/write access<br><br>Modify application orchestration content |Read\-only |Full read/write<br><br>You can modify the content of application orchestration. |Read\-only |
|**Effective environment** |Full read/write<br><br>The application orchestration version can be applied to all environment types. |Full read/write<br><br>The application orchestration version can be made effective for all environment types. |Full read/write<br><br>You can apply the application orchestration version to all environment types. |Full read/write<br><br>The application orchestration version can be applied to all environment types. |Read\-only |
|**configuration** |Read and write<br><br><br>* Has full read and write permissions for configuration items.<br><br>* You have full read and write permissions for Environment configuration. |Read/write<br><br><br>* Has full read and write permissions for configuration items.<br><br>* Has full read and write permissions for environment configuration. |Read\-only |Read/write access<br><br><br>* Has full read and write permissions for configuration items.<br><br>* Full read and write permissions for environment configuration. |Read\-only |
|**settings** |Full read/write<br><br><br>* Basic information about the application can be modified.<br><br>* Deletable applications.<br><br>* Manage members and grant permissions |Half\-duplex<br><br>Basic application information can be modified. |Read\-only |Half\-duplex<br><br>You can modify the application's basic information. |Read\-only |
