---
title: "IAM overview"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/IAM-Overview"
---

Identity and Access Management (IAM) is a system for permission management and is one of the **Free services** provided by the platform. You can create IAM users for your account (root user) and grant them corresponding permissions based on different purposes, controlling access to cloud resources for different identities, achieving decentralized resource management, enhancing management efficiency, and reducing the risk of information leakage.

<span id=".5Li65LuA5LmI5L2_55SoSUFN"></span>
## Why use IAM

Before using any resources, you must first Register an account on the platform. After completing registration, you will obtain an account, which is referred to as the root user. **The root user is automatically granted full administrative privileges over all resources under it by default**.

Using only the main account to manage resources may cause the following issues:


* Multiple people share the main account for actions, making it impossible to identify the actual user.

* The main account has extensive permissions, so any exposure would have severe consequences.

* Using the main account directly for operation and maintenance (O&M) tasks involves higher risks.


You can address these concerns by using the IAM feature. Under the root user, you can create IAM users, user groups, and roles. Newly created IAM users, user groups, and roles initially have no permissions. You can grant appropriate permissions based on their intended use cases, enabling multi\-identity management, granular permission controls, and more.

&nbsp;
