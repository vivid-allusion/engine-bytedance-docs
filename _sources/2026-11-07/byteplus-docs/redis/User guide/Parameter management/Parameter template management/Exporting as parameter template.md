---
title: "Exporting as parameter template"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/export-parameter-template"
---

Cache for Redis supports parameter template export, allowing you to export the configuration of all parameters in the current instance as a parameter template, so you can quickly apply the parameter configuration of the instance to other instances with the same database version by exporting the parameter template.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance.

4. On the instance details page, click the **Parameters** tab.

5. On the **Parameter** sub\-tab, click **Export as template**.

6. In the pop\-up dialog box, configure the following parameters.

   |Parameters |Required? |Description |
   |---|---|---|
   |Template name |Yes |Enter the name of the parameter template. The name needs to meet the following requirements simultaneously:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 2 to 64 characters. |
   |Template description |No |Enter the remarks for the parameter template whose length cannot exceed 200 characters. |
   |Database version |No |No configuration is required. It has the same database version as the current instance.<br><br>After exporting the configuration as a parameter template, this version becomes the supported database version for the parameter template. |

7. Click **OK**.
