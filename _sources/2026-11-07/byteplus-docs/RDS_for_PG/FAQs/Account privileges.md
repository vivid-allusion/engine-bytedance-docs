---
title: "Account privileges"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/account_permissions"
---

This topic summarizes frequently asked questions about RDS for PostgreSQL account permissions.

<span id=".6auY5p2D6ZmQ6LSm5Y-35ZKM5pmu6YCa6LSm5Y-35pyJ5LuA5LmI5Yy65Yir77yf"></span>
### **What are the differences between a super account and a normal account?** 


* Super account: You can create multiple. A super account can manage all normal accounts and databases.

* Normal account: You can create multiple. You need to manually grant specific database permissions to a normal account.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For specific information on account privileges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account">Creating an account</a>.</div>


<span id=".6auY5p2D6ZmQ6LSm5Y-36IO95ZCm5L-u5pS55oyH5a6a5p2D6ZmQ77yf"></span>
### **Can I modify a specific permission of a super account?** 

The super account can only be reset to the initial status, not modified to specific permissions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For specific information on account privileges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/creating_and_managing_an_account">Creating an account</a>.</div>


<span id=".5pWw5o2u5bqT5piv5ZCm5Y-v5Lul57uR5a6a5aSa5Liq6LSm5Y-377yf"></span>
### **Can a database be associated with multiple accounts?** 

You can associate only one account to a database.

<span id="Lner8Ulf"></span>
### How to grant privileges for a single schema?

The Console only supports global‑level privilege grants. If you want to grant privileges on a single schema, you need to use SQL statements. For example, to grant user the permission to use demo_schema, execute the statement `GRANT USAGE ON SCHEMA demo_schema TO user;`.

<span id="mLiSlYw8"></span>
### Will the table owner be updated synchronously after the Schema owner is modified via the Console?

No. Modifying the owner of a schema does not synchronously update the owners of tables within that schema. To modify table owners, SQL statements are required for separate updates. For example: `ALTER TABLE table_name OWNER TO new_owner;`.
