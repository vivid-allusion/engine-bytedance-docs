---
title: "Network connection"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/network_connection"
---

This topic summarizes frequently asked questions about RDS for PostgreSQL network connections.

<span id=".5Li65LuA5LmI5peg5rOV6L-e5o6l5pWw5o2u5bqT77yf"></span>
#### Why can't I connect to the database?

If you cannot access a database, please conduct troubleshooting as recommended:


1. Confirm whether the PostgreSQL instance is in the **Running** state.

2. Confirm whether you have [Created a database and account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_databases_and_accounts) for the instance.

3. Confirm whether [IP allowlists](https://docs.byteplus.com/en/docs/RDS_for_PG/configuring_an_allowlist) are configured.

4. If you are using a private network connection, confirm whether the ECS instance and database instance are in the same VPC.


If the issue persists after troubleshooting, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

<span id=".5aaC5L2V5aSE55CG5LqR5pWw5o2u5bqTIFBvc3RncmVTUUwg54mI5o6n5Yi25Y-w55qE6ZSZ6K-v5o-Q56S677yf"></span>
#### How should I handle error prompts in the RDS for PostgreSQL console?

**Problem description**

You may run into error prompts in the console when you use RDS for PostgreSQL services.

**Solution**

[Submit a ticket](https://console.byteplus.com/workorder/create) in BytePlus and include the RequestId indicated in the error prompt.
