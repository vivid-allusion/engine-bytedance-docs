---
title: "Access control for RDS for MySQL Based on IAM authentication"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Access_control_for_RDS_for_MySQL_Based_on_IAM_authentication"
---

<span id="DWlWPe3j"></span>
## Introduction

With the growing adoption of AI Agents and automation tools, the authentication process for database connections is being re\-evaluated. Traditional password verification cannot meet security needs for temporary authorization, least privilege, and security audits. IAM database authentication has become the mainstream choice for cloud databases. This topic introduces the **IAM authentication capability** of RDS for MySQL.

<span id="0wLdquJR"></span>
## Why use IAM authentication?

In traditional database connection methods, developers write database accounts and passwords in plaintext in configuration files, CI/CD variables, or code repositories. While this method is simple and convenient, it poses significant security risks, such as:


* **Password leakage**: Writing passwords in repositories or logs causes "permanent leakage". Even if developers modify the database account password, existing security risks cannot be completely eliminated.

* **Account privilege abuse**: Developers often use super accounts to operate the database and do not assign privileges to different roles based on their responsibilities. They also fail to recycle account privileges promptly after personnel or business changes.

* **High cost of modifying passwords**: After modifying a database account password, you must also update the configuration in the business code and restart the service. This process is long, cumbersome, and costly.


With the growing adoption of AI Agents and automation tools, the aforementioned security risks will be further amplified in AI Agent scenarios. When developers use the Agent tool to access the database, they do not want to expose the long\-term password in its plain text within the tool, nor do they want to manually enter the password each time they connect to the database. Instead, they hope to use  **"on\-demand acquisition, automatic expiration and recycling, and centralized management by IAM"**  for temporary credentials to access the database.

To address these security risks and meet developers' security needs, RDS for MySQL provides the **IAM DB Authentication** feature. It replaces the **password** required for database connections with a **temporary token** issued by Identity and Access Management (IAM). This temporary token requires an expiration time, and its privileges are centrally managed by the IAM system, fundamentally resolving the security risks of long\-term passwords.

<span id="w3RhQLBy"></span>
## IAM authentication for RDS for MySQL

The IAM authentication feature for RDS for MySQL is designed to achieve the following two goals:


* **Establish a unified database identity system:**  accounts, privileges, and audits are all centrally managed by IAM.

* **Improve database connection capabilities for AI scenarios:**  enable agent tools and automated tasks to use temporary tokens to access the database for on\-demand use.


In terms of product experience, we want the IAM authentication capability to better align with developer habits. Whether generating a temporary Token in the console or obtaining a temporary token directly in application code via an SDK, we aim to minimize migration costs and provide an out\-of\-the\-box experience.

<span id="LLKA9pon"></span>
## Product form: From activation to usage

The IAM authentication capability for RDS for MySQL is available on the following pages:


* **Create account page: new 'Verification method' option**


When creating a database account, developers can select a verification method based on their business needs:


* **Password verification** (Default): A password is required for the database account, and the account and password must be entered in plaintext when connecting to the database.

* **IAM verification**: A password is not required for the database account. When connecting to the database, verification is completed by using a temporary Token generated for the account.


Note

**IAM verification** is not supported for **super accounts** to prevent high\-privilege credentials from being mistakenly included in the temporary token system.


* **The Accounts page now has a 'Verification method' column and a 'Generate temporary token' button.** 


On the Accounts page, the list now includes a 'Verification method' column, allowing database administrators to identify the verification method for each database account at a glance. If a database account's verification method is IAM verification, a **Generate temporary token** button is added to the Actions column **. ** After clicking the button, a temporary token is generated, and you need to select its validity period. A new temporary token is generated with each click, and historical tokens are not saved, but you can download the temporary token.


* **Generating tokens with an SDK: a method more familiar to developers**


Developers can use the SDK to generate a temporary token and pass it as a password to the MySQL client, minimizing the cost of modifying the application code. Example as follows:


* Generating a temporary token


```Shell
# 通过BytePlus SDK 获取临时 Token（伪示例）
TOKEN=$(volc rds generate-db-auth-token \
  --region cn-beijing \
  --instanceId mysql-74dsxxxxxx \
  --dbUser mysql_test \
  --expires 600)
```



* Pass the temporary token to the MySQL client as a password:


```Shell
# 使用 Token 作为密码连接
mysql -h$RDSHOST -umysql_test --enable-cleartext-plugin -p$TOKEN
```


<span id="4GeRFBBI"></span>
## Summary

Database passwords are simple to configure and have been a standard database verification method for many years. However, in today's cloud\-native and AI era, passwords are becoming increasingly cumbersome. Although they are valid long\-term and do not expire, they cannot be audited for security and make it difficult to enforce the principle of least privilege.

**IAM authentication** does more than replace the database password with a temporary token. It upgrades database authentication from a password\-based credential model to an integrated, unified identity system where the IAM system centrally manages, audits, and revokes all connection requests upon expiration. With the growing trend of AI agents and automation tools regularly accessing databases, the security value of a unified identity system becomes even more important.

The IAM authentication capability of RDS for MySQL is designed to be a more secure and elegant way for you to interact and communicate with your database.
