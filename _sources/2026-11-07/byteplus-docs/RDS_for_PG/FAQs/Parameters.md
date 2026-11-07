---
title: "Parameters"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/parameters"
---

This topic summarizes frequently asked questions about RDS for PostgreSQL parameters.

<span id=".5Y-C5pWw566h55CG5Li65LuA5LmI5om-5LiN5Yiw6ZyA6KaB5L-u5pS555qE5Y-C5pWw77yf"></span>
#### **Why can't I find the parameters to modify in parameter management?** 

For security and stability reasons, only some parameters can be modified currently; if you cannot find the parameters to modify, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

<span id=".5L-u5pS55Y-C5pWw5ZCO77yM6ZyA6KaB6YeN5ZCv5a6e5L6L5ZCX77yf"></span>
#### **Does the instance need to be restarted after modification of parameters?** 

Some parameters require restarting the instance after modification. You can check in the console's **Modify parameters** page [whether restart instance is needed](https://docs.byteplus.com/en/docs/RDS_for_PG/restarting_an_instance). For detail, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Operate during business off\-peak hours and ensure the application has a reconnection mechanism.</div>
