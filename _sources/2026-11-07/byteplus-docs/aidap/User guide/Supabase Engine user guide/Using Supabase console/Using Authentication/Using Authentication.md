---
title: "Using Authentication"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Using_Authentication"
---

This topic introduces how different roles use the Authentication function module.

## Background

The feature modules in Supabase console provide different methods for various roles in the application development process.

**Role**

As a BaaS service, the feature modules in Supabase console serve different roles in the application development process: app developers and app users.

**Method**

The Authentication function in the Supabase console can be configured and used on the console and also served through two types of APIs.

* Admin API: refers to the management API configured by app developers for Supabase, requiring `SERVICE_ROLE_KEY`.

* Client API: refers to the API accessed by app users in Supabase, usually called after login.

Methods and examples of calling Admin API and Client API are as follows.

|**API type** |**User** |**Function** |**Methods and examples** |
|---|---|---|---|
|Admin API<br><br> |App developer<br><br> |Configure Auth\-related parameters<br><br> |* Example for querying configuration<br><br><br>```Bash```<br>```# querying configuration```<br>```curl -X GET $SUPABASE_BASE_URL/auth/v1/config \```<br>```  -H "apikey: ${SERVICE_ROLE_KEY}" \```<br>```  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \```<br>```  -H "Content-Type: application/json"```<br><br><br><br>* Example of modifying configuration<br><br><br>```Bash```<br>```curl -X PATCH $SUPABASE_BASE_URL/auth/v1/config \```<br>```  -H "apikey: ${SERVICE_ROLE_KEY}" \```<br>```  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}" \```<br>```  -H "Content-Type: application/json" \```<br>```  -d '{```<br>```       "SMTP_HOST": "smtp.qq.com",```<br>```       "SMTP_USER": "test-user",```<br>```       "SMTP_PASS": "test-paas"```<br>```      }'```<br> |
|Client API<br><br>( Supabase Client SDK) |App users |Access auth (register, login, etc.) in the app frontend |* Registration example<br><br><br>```JavaScript```<br>```import { createClient } from '@supabase/supabase-js'```<br>```const supabase = createClient(```<br>```  "<SUPABASE_BASE_URL>",```<br>```  "<SUPABASE_ANON_KEY>")```<br>``````<br>```// email registration```<br>```async function signUp() {```<br>```  const { data, error } = await supabase.auth.signUp({```<br>```    email: 'user@example.com',```<br>```    password: 'password123'```<br>```  })```<br>``````<br>```  if (error) {```<br>```    console.log('注册失败:', error.message)```<br>```    return```<br>```  }```<br>```  console.log('注册成功，请查收邮箱验证', data)```<br>```}```<br><br><br><br>* Login example<br><br><br>```JavaScript```<br>```import { createClient } from '@supabase/supabase-js'```<br>```const supabase = createClient(```<br>```  "<SUPABASE_BASE_URL>",```<br>```  "<SUPABASE_ANON_KEY>")```<br>``````<br>```// account and password login```<br>```async function signIn() {```<br>```  const { data, error } = await supabase.auth.signInWithPassword({```<br>```    email: 'user@example.com',```<br>```    password: 'password123'```<br>```  })```<br>``````<br>```  if (error) {```<br>```    console.log('登录失败:', error.message)```<br>```    return```<br>```  }```<br>```  console.log('登录成功', data.user)```<br>```}```<br> |
