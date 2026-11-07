---
title: "Using Database"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Using_Database"
---

This topic introduces how different roles use the Database function module.

<span id="xPTVemYx"></span>
## Background

The feature modules in Supabase console provide different methods for various roles in the application development process.

**Role**

As a BaaS service, the feature modules in Supabase console serve different roles in the application development process: app developers and app users.

**Method**

The Supabase console's database function provides services through two types of APIs.


* The admin API refers to the management API configured by app developers for Supabase, requiring `SERVICE_ROLE_KEY`.

* The client API refers to the API accessed by app users in Supabase, usually called after login.


Methods and examples of calling Admin API and Client API are as follows.


|**API type** |**User** |**Function** |**Method and example** |
|---|---|---|---|
|admin API (HTTP interface)<br><br> |App developer |Execute initialization DDL, DML, etc.<br><br> |* You can use `/postgres/query` to execute DDL and DML.<br><br>* You can also execute DDL using other interfaces under `/postgres/` (e.g., `tables`, `columns`). Refer to [postres-meta](https://github.com/supabase/postgres-meta).<br><br>* Execute DDL example<br><br><br>```Bash```<br>```Execute DDL```<br>```curl -X POST $SUPABASE_BASE_URL/postgres/query \```<br>```  -H "apikey: ${SERVICE_ROLE_KEY}" \```<br>```  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \```<br>```  -H "Content-Type: application/json" \```<br>```  -d '{"query": "CREATE TABLE foo(id serial primary key, name text);"}'```<br><br><br><br>* Execute DML example<br><br><br>```Bash```<br>```# Execute DML```<br>```curl -X POST $SUPABASE_BASE_URL/postgres/query \```<br>```  -H "apikey: ${SERVICE_ROLE_KEY}" \```<br>```  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \```<br>```  -H "Content-Type: application/json" \```<br>```  -d '{"query": "insert into table foo values(1, 'aaa');"}'```<br> |
|admin API (HTTP interface)<br><br> |App developer |Query and modify Data API configuration<br><br>(Located at Supabase console: **Project Settings** \> **Data API**)<br><br> |* Query Data API configuration<br><br><br>```Bash```<br>```Query Data API configuration```<br>```curl -X GET $SUPABASE_BASE_URL/rest/v1/config \```<br>```  -H "apikey: ${SERVICE_ROLE_KEY}" \```<br>```  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \```<br>```  -H "Content-Type: application/json"```<br><br><br><br>* Modify Data API configuration<br><br><br>```Bash```<br>```Modify Data API configuration```<br>```curl -X PATCH $SUPABASE_BASE_URL/rest/v1/config \```<br>```  -H "apikey: ${SERVICE_ROLE_KEY}" \```<br>```  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \```<br>```  -H "Content-Type: application/json" \```<br>```  -d '{```<br>```    "db_schema": "public,graphql_public,vault",```<br>```    "db_extra_search_path": "extensions,graphql_public,vault",```<br>```    "max_rows": 200```<br>```  }'```<br> |
|Client API (Supabase Client SDK)<br><br> |App users |Access Database in the app |```JavaScript```<br>```import { createClient } from '@supabase/supabase-js'```<br>```const supabase = createClient(```<br>```  "<SUPABASE_BASE_URL>",```<br>```  "<SUPABASE_ANON_KEY>")```<br>``````<br>```async function find() {```<br>```  const { data, error } = await supabase```<br>```    .from('students')```<br>```    .select('*')```<br>```    .eq('name', 'tom')```<br>```    .gt('age', 18)```<br>```  ```<br>```  if (error) {```<br>```    console.error('failed: ', err.message)```<br>```  } else {```<br>```    console.log('success: ', data)```<br>```  }```<br>```}```<br> |
|Client API (HTTP interface)<br><br> |App users |Access Database in the app<br><br> |```Bash```<br>```# example of querying table data using curl```<br>```curl -X GET $SUPABASE_BASE_URL/rest/v1/users?id=eq.xxx \```<br>```  -H "apikey: ${ANON_KEY}" \```<br>```  -H "Authorization: Bearer ${ACCESS_TOKEN}" \```<br>```  -H "Content-Type: application/json"```<br>```  -H "Prefer: return-representation"```<br><br><br>```JavaScript```<br>```// js example of modifying table data```<br>```const updateUser = async (userId, updates): =>```<br>```    const response = await fetch(`${SUPABASE_BASE_URL}/rest/v1/users?id=eq.${userId}`, {```<br>```        method: 'PATCH',```<br>```        headers: {```<br>```            'apikey': '${ANON_KEY}',```<br>```            'Authorization': 'Bearer ${ACCESS_TOKEN}',```<br>```            'Content-Type': 'application/json',```<br>```            'Prefer': 'return=representation'```<br>```        },```<br>```        body: JSON.stringify(updates)```<br>```    };```<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><code>${ACCESS_TOKEN}</code> is automatically obtained after the app user logs in successfully.</div><br> |
