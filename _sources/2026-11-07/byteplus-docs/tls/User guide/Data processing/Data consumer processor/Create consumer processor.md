---
title: "Create consumer processor"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Create_consumer_processor"
---

This topic describes how to create a consumer processor.

## Prerequisites

* A project has been created. For detailed steps, see [Log project](https://docs.byteplus.com/docs/tls/Managing_projects).

* Data transformation permissions for TLS have been obtained. For details, see [Authorized actions](https://docs.byteplus.com/docs/tls/Authorizable_actions).

## Steps

1. Log in to [TLS console](https://console.byteplus.com/tls).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation bar, select **Data processing** \> **Data processor**.

4. Click  **+**  icon under the **consumer processor** tab to open the **Create consumer processors** page.

   ![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/91a80724d45b4620862657088c23694d)

5. Configure the basic information for the consumer processor.

   |Parameters |Description |
   |---|---|
   |Log project |The project to which the consumer processor belongs.<br><br>The consumer processor only supports associating log topics within this project and does not support cross\-project operations. |
   |Name |Data processor name. |
   |Description |Data processor description. |
   |Failure handling policy |Policy for handling invalid log data configurations.<br><br><br>* Retain original data sources and write directly<br><br>* Discard original data source |

6. Write data processing rules.

   Follow the onscreen instructions to enter processing rules in the input box. TLS supports a variety of DSL syntax functions. On the transformation functions tab, you can click a function name to view syntax descriptions and examples, and insert specified syntax with one click to quickly write transformation rules. For the list of supported syntax functions, see [Functions overview](https://docs.byteplus.com/docs/tls/overview_of_functions).

7. Test data processing rules.

   Follow the page instructions to test by using log data from the log topic or specified test data. Click **Preview execution** to test transformation rules.

   * If the page prompts **DSL code compilation failed**, it means the transformation statement contains errors. You can refer to the error information provided and fix the syntax issue in the specified line, and then retest the transformation rule.

   * If the data transformation result is correct, click **Create consumer processor**.

8. Select a startup strategy for the consumer processor.

   In the pop\-up **Start immediately after task creation** dialog, select whether to activate the consumer processor right away.

   * **Immediately start**: The consumer processor will launch immediately after configuration is complete.

   * **Enter pause mode**: The consumer processor will not launch automatically after configuration. You can manually start the task as needed. For details, see [Manage consumer processor](https://docs.byteplus.com/docs/tls/Manage_consumer_processor).

   * **Cancel**: Cancel the creation of the consumer processor.
