---
title: "Constraints and limits"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Constraints_and_limits"
---

AI Native BaaS for Supabase relies on the AI Native Database Platform (AIDAP) and provides services through two database engines: Supabase and PostgreSQL This topic introduces the usage constraints and limitations of the PostgreSQL engine and the Supabase engine within the AI Native Database Platform.

## PostgreSQL engine usage suggestions

For workspaces using the PostgreSQL engine, to achieve stable performance and resource usage experience, it is recommended to refer to the following recommended values during business planning and usage. When business scales significantly exceed the recommended values, performance fluctuations or resource shortages may occur; capacity evaluation should be conducted in advance.

|**Item** |**Constraints** |
|---|---|
|Transactions Per Second (TPS) |It is recommended that the TPS of each branch does not exceed 10. |
|Queries Per Second (QPS) |It is recommended that the QPS of each branch not exceed 20. |
|Current active connections |It is recommended that the number of active connections per branch does not exceed 10. |
|Data volume |It is recommended to control the data volume of each branch below 10 GB. |
|Number of roles |It is recommended that the number of roles in each branch not exceed 50. |
|Total number of databases |It is recommended that the number of databases per branch does not exceed 50. |
|Number of schemas |It is recommended that the number of schemas per branch does not exceed 100. |
|Number of tables per database |It is recommended that the number of tables per database does not exceed 1000. |
|Branches |It is recommended that the number of branches in each workspace not exceed 10. |
|Business table data capacity upper limit |Related to the upper limit of compute expansion range (Max CU), details as follows:<br><br><br>* Max CU ≤ 2C: storage capacity upper limit 120 GB<br><br>* Max CU ≤ 16C: storage capacity upper limit 240 GB<br><br>* Max CU ≤ 32C: storage capacity upper limit 480 GB<br><br><br>After modifying the upper limit of the compute expansion range, the storage capacity upper limit also adjusts accordingly. |

## Usage limits and suggestions for Supabase engine

### Usage restrictions

Key limits of the Supabase version in workspace branches, authentication, database, object storage, edge functions, logs, and network; pay attention to the corresponding constraints when creating and using resources.

|**Item** |**Constraints** |
|---|---|
|The number of branches in the workspace |It is recommended that the number of branches per workspace does not exceed 10. Refer to [note for creating a branch](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_branch) for details. |
|Auth Third\-Party Provider |Supabase Auth supports third\-party Auth access based on Sign In / Providers. Refer to related [notes](https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_third-party_login#3YMdT4Ga) before use, including compatibility with third\-party identity services and JWT verification configuration. |
|Auth Hooks |Supabase Auth Hooks support passing JWT Token and various Hook types. Focus on its [constraints](https://docs.byteplus.com/en/docs/aidap/Supabase-Configuring_Auth_Hooks?lang=en#y1kjHx7Z) before use to avoid login and callback process abnormalities caused by improper configuration. |
|Database |* For PostgreSQL engine\-related recommendations, refer to the above [PostgreSQL engine usage recommendations](https://docs.byteplus.com/en/docs/330/106241#iieB9dvA).<br><br>* The maximum number of database tables per single branch created through Table Editor is 10,000. |
|Storage Object |The default maximum size for a single file is 50 MB, adjustable up to 51200 MB (50 GB). |
|Edge Function |The default upper limit of edge functions per Supabase branch is 500. |
|Log retention days |The log retention days default to 30 days. |
|Shared public network bandwidth of a single branch |The bandwidth limit for shared public network addresses is 100 Mbps. |
|Branch memory |Ordinary newly created branches do not inherit memory from the parent branch. |
|Memory migration |The initial version does not support importing, exporting, or cross\-branch copying of memory. |
|Memory retention |Memory by default does not expire and has no quantity limit. If no longer needed, delete it actively. |
|Business user deletion |Deleting a business user does not automatically clear the user’s memory; it must be deleted separately. |
|Business table data capacity upper limit |Related to the upper limit of compute expansion range (Max CU), details as follows:<br><br><br>* Max CU ≤ 2C: storage capacity upper limit 120 GB<br><br>* Max CU ≤ 16C: storage capacity upper limit 240 GB<br><br>* Max CU ≤ 32C: storage capacity upper limit 480 GB<br><br><br>After modifying the upper limit of the compute expansion range, the storage capacity upper limit also adjusts accordingly. |

### Usage suggestion

In addition to the above mandatory or recommended restrictions, you can also refer to the following usage suggestions when using the Supabase version daily to enhance service security and scalability.

#### Properly store related passwords or keys

Keep Supabase\-related passwords, keys, and others properly to avoid exposure and security risks. Including but not limited to:

* service_role_key of Supabase.

* Password for the postgres account in Supabase PostgreSQL.

* Password or key in Supabase edge function secrets.

* Login account and password for Supabase dashboard.

* Private key for the custom JWKS in Supabase Auth Third\-Party.

**Security note:**  if the above keys are leaked externally, it may lead to unauthorized database access or sensitive data being read or tampered with. It is recommended to use enterprise internal key management services (KMS) or Vault\-like tools for centralized storage and regular rotation.

#### Increase the quota for the private network elastic network interface (ENI) and expand the subnet network segment.

Generally, if a Supabase branch enables private network addresses, each branch binds an independent [virtual private cloud (ENI)](https://docs.byteplus.com/en/docs/vpc/Network-interface-overview) and occupies one IP under the selected subnet.

For scenarios like vibe coding that require batch creation of instances and branches, shortage of elastic network card quota or insufficient IP addresses under the subnet may be encountered. The following measures are recommended for advance planning:

1. **Increase virtual network card quota in advance.**  For detailed operations, refer to [Initiate quota change application and view application history](https://docs.byteplus.com/en/docs/resourcemanagement/Initiate_Quota_Change_Application_and_View_Application_History). The quota item path is: "Network" → "Virtual Private Cloud" → "eni". It is also recommended to [Create quota alert](https://docs.byteplus.com/en/docs/resourcemanagement/Create_Quota_Alert) to monitor remaining quota timely.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63ac6de44f84178ea83b94e008976333.png)

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4f42507773b87a2c2bdc40e0689abc69.png)

2. **Plan the VPC and subnet network segment sizes reasonably.**  When creating VPC and subnet, select the appropriate network segment based on business scale (the smaller the mask, the larger the segment). It is recommended that the Subnet mask does not exceed 16 to accommodate the private network IPs required by a large number of branches.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5aa73f05b8efc81ef5539def00d233f5.png)

> If hundreds or thousands of Supabase branches are expected to run within a single VPC, it is recommended to complete ENI quota application and subnet segment planning early in the project to avoid migration costs caused by adjustments after business launch.
