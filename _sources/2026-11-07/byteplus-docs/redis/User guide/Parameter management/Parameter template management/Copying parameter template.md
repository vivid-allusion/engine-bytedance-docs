---
title: "Copying parameter template"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/copy-parameter-template"
---

If you need to create a new parameter template, but most of the parameters and values in an existing parameter template match those of the new one, you can quickly create the new template by copying the existing one and then editing it as needed. This topic describes how to copy parameter template.

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. In the left\-side navigation pane, select **NoSQL Database \> Redis \> Parameter templates**.

4. On the **Parameter templates** page, choose the appropriate steps depending on the type of parameter template you want to copy.

   * Copy customized template

      On the **Customized templates** tab, find the target template you want to copy in the template list, and click **Copy** in the **Actions** column on the right.

   * Copy system template

      1. Click the **System templates** tab.

      2. In the system template list, find the target template to be copied, and click **Copy** in the **Actions** column on the right.

5. In the pop\-up dialog box, configure the following parameters.

   |Parameters |Required? |Description |
   |---|---|---|
   |Template name |Yes |Enter the name of the parameter template. The name needs to meet the following requirements simultaneously:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length should be 2 to 64 characters. |
   |Template description |No |Enter the remarks for the parameter template whose length cannot exceed 200 characters. |

6. Click **OK**.

## Subsequent operations

After successfully copying the parameter template, you can edit and modify the settings in the new template and apply the modified template to instances. For specific procedures, refer to [Editing parameter template](https://docs.byteplus.com/en/docs/redis/edit-parameter-template) and [Applying parameter template](https://docs.byteplus.com/en/docs/redis/apply-parameter-template).
