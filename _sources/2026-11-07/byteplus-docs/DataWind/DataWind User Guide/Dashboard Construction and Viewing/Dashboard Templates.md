---
title: "Dashboard Templates"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dashboard_Templates"
---

Intelligent Data Insights provides private deployment users with a variety of dashboard template options. This article introduces how to use official dashboard templates, how to export self\-built dashboards as templates, and how to use and manage templates.

<span id="_1-概述"></span>
# Feature overview

Users can load and apply official dashboard templates with one click, replace the datasets in the templates with their own data to make the templates their own, and make their dashboards more refined and visually appealing. Users can also create their own templates or use templates within the project.

<span id="d7a895b9"></span>
# Usage restrictions


* After enabling the template capability in a private deployment environment, all users can use the dashboard template feature.

* The dashboard template feature is currently not supported in the SaaS environment.


<span id="_2-私有化部署使用仪表盘模板"></span>
# Use official dashboard templates

<span id="_2-1-前置准备"></span>
## Prerequisites


* Contact Volcano Engine official personnel to enable the dashboard template feature in the target environment and add user accounts that can import templates.

* Obtain the dashboard template file: Click to download the template file and extract it.


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/452ba75ccba1463fa3b9b212d973dbe6~tplv-goo7wpa0wc-image.image" name="Dashboard Templates.zip">Dashboard Templates.zip</Attachment>


&nbsp;

<span id="_2-2-导入仪表盘模板"></span>
## Import dashboard templates


1. Open the "Template Library" in the target environment. The entry is under [Dashboard] \> [Dashboard Templates] in the top navigation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87bde0754f074ea5921b6f0dcdb14ac1~tplv-goo7wpa0wc-image.image) </span>

2. Click the [Import Template] button under the [+] icon. The official templates are in the file mentioned above and can be imported as needed. For details, see [Official Dashboard Templates](https://docs.byteplus.com/docs/DataWind/Official_Dashboard_Templates)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3136327b4a0429184477c4ce635d0cd~tplv-goo7wpa0wc-image.image) </span>

3. Click to upload the template resource package, select the template resource you just downloaded, click Upload, and follow the prompts to proceed to the next step.

4. Select the target directory and click Confirm to complete the template import.

5. You can then see the template list on the dashboard templates page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5839e7961ff48d79926dfa047150108~tplv-goo7wpa0wc-image.image) </span>


<span id="56e43bfe"></span>
# Export self\-built dashboards as templates

Users can export dashboards they have created and desensitize them as templates. Other members with permissions within the project can view the templates and edit, move, or delete them.


1. Enter the dashboard, click the three dots in the upper right corner, and select Export as Template.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ad722c17a48481a9dadfbdfa33e2e5d~tplv-goo7wpa0wc-image.image) </span>

2. In the pop\-up window, you can set data sampling and desensitization. Click Desensitization Rules to configure the desensitization rules.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c114f435f4840d89e7902c27dcee0fe~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80df413cd54a4c08932ce3ad38f44fde~tplv-goo7wpa0wc-image.image) </span>

   The parameter descriptions for desensitization rules are as follows.

   
   |Parameters |Configuration instructions |
   |---|---|
   |Enable desensitization |The user can choose whether to enable desensitization. After enabling desensitization, the field content will be displayed in the dashboard template according to the results processed by the desensitization rules. |
   |Desensitization type |There are two types: text desensitization and numeric desensitization. The rule for text desensitization is "keep the first and last character, and replace the remaining characters with \* "; the rule for numeric desensitization is "multiply by a random number between 1 and 10". |
   


<span id="393e9402"></span>
# Use/manage templates


1. Click the plus sign in the upper left corner and select a dashboard template.

2. Go to the template list, select a template, and click "Apply Template" in the upper right corner to use it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b58b24c7321481eb277ede8c18328e7~tplv-goo7wpa0wc-image.image) </span>

3. Click the "More" option on the left side of the dashboard to move or delete the dashboard.

4. Click the plus sign at the top to import templates or create a new folder to organize templates.
