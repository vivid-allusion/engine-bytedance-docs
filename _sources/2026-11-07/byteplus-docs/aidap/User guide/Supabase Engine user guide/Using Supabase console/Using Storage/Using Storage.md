---
title: "Using Storage"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Use_Storage"
---

This topic introduces how different roles use the storage function module.

<span id="2BCagVtY"></span>
## Background

The feature modules in Supabase console provide different methods for various roles in the application development process.

**Role**

As a BaaS service, the feature modules in Supabase console serve different roles in the application development process: app developers and app users.

**Method**

The Storage feature in the Supabase console can be configured and used on the console and also served through two types of APIs.


* Admin API: refers to the management API configured by app developers for Supabase, requiring `SERVICE_ROLE_KEY`.

* Client API: refers to the API accessed by app users in Supabase, usually called after login.


Methods and examples of calling Admin API and Client API are as follows.


|**API type** |**User** |**Function** |**Methods and examples** |
|---|---|---|---|
|admin API (HTTP interface)<br><br> |App developer<br><br> |Manage bucket, configuration items, etc.<br><br> |1. Create bucket<br><br><br>```Bash```<br>```# curl example to query the bucket list```<br>```curl -X POST $SUPABASE_BASE_URL/storage/v1/bucket \```<br>```  -H "apikey: ${SERVICE_ROLE_KEY}" \```<br>```  -H "Authorization: Bearer ${SERVICE_ROLE_KEY}"```<br>```  -H 'Content-Type: application/json' \```<br>```  -d '{```<br>```       "name": "my-bucket",```<br>```       "public": false,```<br>```       "file_size_limit": "100MB",```<br>```       "allowed_mime_types": ["image/png", "image/jpeg"]```<br>```     }'```<br><br><br><br>2. Modify configuration<br><br><br>```Bash```<br>```# example of curl configuration parameters```<br>```# parameter fileSizeLimit indicates the single file size (in bytes).```<br>```# parameter totalFileSizeLimit indicates the total size limit of all files (unit: byte)```<br>```curl -X PATCH $SUPABASE_BASE_URL/storage/v1/config \```<br>```  -H "apikey: ${SERVICE_ROLE_KEY}" \```<br>```  -H 'Authorization: Bearer ${SERVICE_ROLE_KEY}' \```<br>```  -H 'Content-Type: application/json' \```<br>```  -d '{```<br>```       "fileSizeLimit": 52428800,```<br>```       "totalFileSizeLimit": 5368709120```<br>```      }'```<br> |
|Admin API (Supabase Client SDK)<br><br> |App developer |Manage bucket, configuration items, etc. |Besides directly using the HTTP interface, it is recommended to use the Supabase Client SDK combined with `SERVICE_ROLE_KEY` to implement it.<br><br>```JavaScript```<br>```import { createClient } from '@supabase/supabase-js'```<br>```const supabase = createClient(```<br>```  "<SUPABASE_BASE_URL>",```<br>```  "<SUPABASE_SERVICE_ROLE_KEY>")```<br>``````<br>```// create bucket (no try-catch, directly check error)```<br>```async function createBucket() {```<br>```  const { data, error } = await supabase```<br>```    .storage```<br>```    .createBucket('new-bucket', {```<br>```      public: true```<br>```    })```<br>``````<br>```  if (error) {```<br>```    console.error('failed: ', error.message)```<br>```    return```<br>```  }```<br>``````<br>```  console.log('success: ', data)```<br>```  return data```<br>```}```<br> |
|Client API (Supabase Client SDK) |App users |Access Storage in the app frontend |Upload/download object, etc.<br><br>```JavaScript```<br>```import { createClient } from '@supabase/supabase-js'```<br>```const supabase = createClient(```<br>```  "<SUPABASE_BASE_URL>",```<br>```  "<SUPABASE_ANON_KEY>")```<br>``````<br>```// download and convert image example```<br>```async function downloadAndTransformImage() {```<br>```  const { data, error } = await supabase```<br>```    .storage```<br>```    .from('pic-bucket')```<br>```    .download('pic.bmp', {```<br>```      transform: {```<br>```        width: 300,```<br>```        height: 300,```<br>```        quality: 80,```<br>```        format: 'jpg'```<br>```      }```<br>```    })```<br>``````<br>```  if (error) {```<br>```    console.error('failed: ', err.message)```<br>```  } else {```<br>```    console.log('success: ', data)```<br>```  }```<br>```}```<br> |


<span id="OFXSHrIh"></span>
##
