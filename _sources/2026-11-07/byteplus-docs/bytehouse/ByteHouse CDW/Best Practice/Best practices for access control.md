---
title: "Best practices for access control"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/best-practice-for-access-control"
---

This article uses a specific enterprise as an example to introduce the permission control practices when using ByteHouse, and illustrates the ideas and principles of ByteHouse permission control.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For a detailed introduction to ByteHouse's permission control capabilities, refer to <a href="https://docs.byteplus.com/docs/bytehouse/access-control-overview">Overview</a>.</div>


<span id="b4dd3a87"></span>
# Example Scenarios

The example business scenarios below describe an enterprise with a ByteHouse Administrator and multiple business departments, each having several ByteHouse users.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/523db9f8ce584a5b99e11eab82099ad6~tplv-goo7wpa0wc-image.image) </span>

The various departments/personnel in the enterprise and their database table usage are as follows.


|Personnel/Departments |Database |Table |Business Scenarios & Minimum Permission Scope |
|---|---|---|---|
|Department A, which houses multiple users |user |* user.user_info<br><br>* user.access_info |* Business scenario: Department A is the business operations team that routinely views Product's user information and user operation data tables for user operational analysis.<br><br>* Permission scope: Personnel in Department A require "Read" access to user_info and access_info data tables. |
|Department B, which houses multiple users |* product<br><br>* bill |* product.product_info<br><br>* bill.billing_info |* Business Scenario: Department B is the product team, which regularly needs to view product usage data and revenue data for user analysis and product improvement.<br><br>* Scope: Personnel in Department B require "Read" access to the product.product_info and bill.billing_info tables. |
|ByteHouse Administrator |All Databases |All Tables |* Business Scenario: ByteHouse administrators need to manage and maintain all tables, including permissions management.<br><br>* Scope: All permissions of ByteHouse |


<span id="47df7bdb"></span>
# Permission Control Practices

Based on the example scenarios above, this section introduces the best practices for implementing ByteHouse access control via role management.


1. **Main account** creates IAM users and grants IAM permission policies.

   1. The main account creates sub\-users for the ByteHouse Administrator and users in various business departments through the BytePlus IAM.

   2. Bytehouse administrators (DBA or SRE) need to manage Bytehouse instances and grant the ByteHouseFullAccess permission.

   3. Other users only need the ByteHouseReadOnlyAccess permission.

      For activity details, refer to [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management).

2. **ByteHouse administrators** completely isolate the data of different business departments according to the division of responsibilities.

   Grant different ByteHouse environment permissions to business departments A and B to achieve isolation of resources and data through the ByteHouse environment. For details on multi\-environment management, refer to [Manage environment](https://docs.byteplus.com/docs/bytehouse/manage-environment).

3. **ByteHouse administrators** authorize users of business department A.

   1. Create a new "Business Operation" role in Bytehouse with read\-only permissions (select, show) for the user_info and access info tables.

   2. Then, assign this role to the users under department A.

      For operation details, refer to [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration).

4. **ByteHouse Administrator** authorizes department B's user.

   1. Create a new "Product Manager" role in Bytehouse that only has read\-only data permissions (select, show) for the product.product_info, bill.billing_info tables.

   2. Then grant this role to the users under department B.

      For activity details, refer to [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration).


Through the above permission management, you can implement the ByteHouse permission control scenario described in this article.
