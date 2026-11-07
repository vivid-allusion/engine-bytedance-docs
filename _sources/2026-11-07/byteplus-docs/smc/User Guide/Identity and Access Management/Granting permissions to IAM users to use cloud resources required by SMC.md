---
title: "Granting permissions to IAM users to use cloud resources required by SMC"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Authorize-IAM-users-to-use-SMC-dependent-cloud-resources"
---

The root user has full access permissions to all cloud resources under the account. However, in complex cloud scenarios, sharing root user credentials is inconvenient and risky to account security. Therefore, when resources are shared among multiple users, you can use the IAM feature to create IAM users or user groups and grant them specific permissions for cloud resource access as the root user. This enables multi\-identity management and fine\-grained permission control.

This topic describes how to create IAM users or user groups as the root user and grant the minimum permissions required for accessing cloud resources associated with SMC to IAM users or user groups based on needs. This helps achieve delegated management, improve management efficiency, and maintain account security.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You can create users and directly grant permissions to them, or grant user group\-associated permissions to them by adding them to a user group.


<Tabs>
<Tab zoneid="wHyAAQCVBX" title="Grant permissions to IAM user directly">
<TabTitle>Grant permissions to IAM user directly</TabTitle>

1. Log in to theIdentity and Access Management (IAM) console as the root user or an authorized account. Then, create an IAM user.  

2. Assign permission policies related to cloud products required by SMC to the target IAM user. 


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To assign required permission policies, refer to <a href="https://docs.byteplus.com/en/docs/smc/SMC-IAM-policy-types#.U01D5o6n5Yi25Y-w5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl">Roles or policies required by SMC console features</a>.</div>



3. Log in to the platform as the IAM user.

   * **Method 1:** 

      On the user list page of the Identity and Access Management (IAM) console, copy the IAM user login link for the current account and open it to log in directly.

   * **Method 2:** 

      Access the platform login page. Then, click "IAM user" at the lower right of the "Log in now" button to navigate to the user login page. First, enter the account name or ID of the root user, and then enter the IAM username and password for login.


</Tab>
<Tab zoneid="dv9SMysPxR" title="Grant permissions to IAM user by adding IAM user to user group">
<TabTitle>Grant permissions to IAM user by adding IAM user to user group</TabTitle>

1. Log in to the Identity and Access Management (IAM) console as the root user or an authorized account. Then, create a user group. 

2. Assign permission policies related to cloud products required by SMC to the target user group. 


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To assign required permission policies, refer to <a href="https://docs.byteplus.com/en/docs/smc/SMC-IAM-policy-types#.U01D5o6n5Yi25Y-w5Yqf6IO95L6d6LWW55qE6KeS6Imy5oiW562W55Wl">Roles or policies required by SMC console features</a>.</div>



3. Create an IAM user. 

4. Add the IAM user to the user group. 

5. Log in to the platform as the IAM user.

   * **Method 1:** 

      On the user list page of the Identity and Access Management (IAM) console, copy the IAM user login link for the current account and open it to log in directly.

   * **Method 2:** 

      Access the platform login page. Then, click "IAM user" at the lower right of the "Log in now" button to navigate to the user login page. First, enter the account name or ID of the root user, and then enter the IAM username and password for login.


</Tab>
</Tabs>
