---
title: "Configuring and managing Storage"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Configuring_and_managing_Storage"
---

This topic introduces configuring and managing Storage through the Supabase console and the Admin API.

<span id="AvtuLBYL"></span>
## Configure and manage Storage in the Supabase console

<span id="5TXsTJbc"></span>
### Prerequisites


* A workspace using the Supabase engine is created, and its status is **Running**. For more details on creating a workspace, refer to [Creating a workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace).

* The Supabase console has been successfully logged in through the target workspace. For more details on logging in to the console, refer to [Logging into Supabase console](https://docs.byteplus.com/en/docs/aidap/Supabase-Logging_in_to_the_Supabase_console).


<span id="USqBF0VI"></span>
### **Query and modify configurations** in the Supabase console


1. In the Supabase console, click **Storage ** on the left to enter the **Storage** page.

2. On the **Storage** page, click **Configuration** \> **Settings** to enter the **Storage Settings** page. On the **Storage Settings** page:

   * You can view the current configuration information.

   * After modifying the following configurations, click **Save** to complete the configuration changes.

      
      |**Dashboard configuration item name** |**Configuration item Key** |**Configuration item Value type** |**Configuration item description** |**Is it required?**  |**Description of configuration item Value** |
      |---|---|---|---|---|---|
      |Global file size limit<br><br> |fileSizeLimit<br><br> |int (unit: byte) |Single file size limit |No |* Maximum value: 51,200 MB.<br><br>* Default value: 52,428,800 (50 MB) |
      |Total file size limit for all buckets |totalFileSizeLimit |int (unit: byte) |Total capacity limit of all buckets |No |* Maximum value is 10,485,760 MB (10,240 GB).<br><br>* Default is 5,368,709,120 (5 GB)<br><br>* value \-1 indicates unlimited. |
      


<span id="fgOSdIXX"></span>
## Configure and manage Storage via Admin API

<span id="o1rUYaln"></span>
### Prerequisites

Obtained `SUPABASE_BASE_URL`, `SERVICE_ROLE_KEY`, and `SUPABASE_ANON_KEY`. For more information on obtaining variables, refer to [Obtaining variables](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_variables).

<span id="48bP4rJG"></span>
### **Query and modify configuration via Admin API**


* Query configuration


```Bash
curl -X GET $SUPABASE_BASE_URL/storage/v1/config \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H 'Authorization: Bearer ${SERVICE_ROLE_KEY}'
```



* Modify configuration


```Bash
# example of curl configuration parameters
# parameter fileSizeLimit indicates the single file size (in bytes).
# parameter totalFileSizeLimit indicates the total size limit of all files (unit: byte)
curl -X PATCH $SUPABASE_BASE_URL/storage/v1/config \
  -H "apikey: ${SERVICE_ROLE_KEY}" \
  -H 'Authorization: Bearer ${SERVICE_ROLE_KEY}' 
  -H 'Content-Type: application/json' \
  -d '{
       "fileSizeLimit": 52428800,
       "totalFileSizeLimit": 5368709120
      }'
```


<span id="iAHl0Imq"></span>
###
