---
title: "Exporting parameter list from parameter template"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/export-parameter-list-from-parameter-template"
---

Cache for Redis supports exporting the parameter template to local in TXT file format. In the TXT file, all the configured parameter names and parameter values in the current template will be displayed in the form of `ParameterName=value`, which facilitates you to create a new parameter template based on the parameters in the current parameter template. This topic describes how to export parameter list from a parameter template on the Redis console.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left\-side navigation pane, select **NoSQL Database \> Redis \> Parameter templates**.

4. On the **Parameter templates** page, under the **Customized templates** or **System templates** tab, click the name of the parameter template you want to export.

5. In the **Parameter template details** control panel, click ![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg) icon in the upper right corner of the parameter list.

   > **tip**

   > After clicking ![](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg)  icon, the system will automatically save all the configured parameter names and parameter values in the current parameter template in a TXT file in the form of `ParameterName=value`. The file name format is r`edis_<database version applicable to the parameter template>_<parameter template name>.txt` (for example, `redis_5.0_paratemp.txt`).

## Subsequent operations

You can copy the required parameter configurations from the parameter template TXT file downloaded to your local device. Then, when creating a new parameter template, select **Add parameters in batches**, and paste the parameter configuration information copied just now in the pop\-up **Add parameters in batches** dialog box. For specific procedures, refer to [Creating parameter template](https://docs.byteplus.com/en/docs/redis/create-parameter-template).
