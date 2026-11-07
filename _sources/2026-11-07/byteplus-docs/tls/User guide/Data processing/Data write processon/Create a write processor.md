---
title: "Create a write processor"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Create_a_data_processor"
---

This document describes how to create a write processor.

## Prerequisites

A log project has been created. For detailed steps, see [Log project](https://docs.byteplus.com/docs/tls/Managing_projects).

## Procedure

1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region for TLS.

3. In the left navigation pane, select **Data Processing** \> **Data Processor**.

4. In the write processor list, click  **+**  to go to the **Create Write Processor** page.

   ![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/06de955b8d464656887d48e607147f64)

5. Configure the basic information for the write processor.

   |Parameters |Description |
   |---|---|
   |Project |The project to which the write processor belongs.<br><br>The write processor only supports associating log topics within this project and does not support cross\-project associations. |
   |Name |Name of the write processor. |
   |Description |Description of the write processor. |
   |Failure handling policy |Policy for handling invalid log data.<br><br><br>* Retain original data and write directly<br><br>* Discard original data |

6. Write data transformation rules.

   Enter the data transformation rules in the input box as prompted on the page. TLS supports various DSL syntax functions. You can click the function name on the transformation functions tab to view syntax descriptions and examples, and you can also insert the specified syntax with one click to quickly write transformation rules. For a list of supported syntax functions, see [Functions overview](https://docs.byteplus.com/docs/tls/overview_of_functions).

   > **Note**

   > The following functions in the function list are currently not supported:

   * > Event handling functions: e_output function, e_auto_output function.

   * > Resource function: res_rds_mysql function.

7. Test the data transformation rules.

   Test using log data from the log topic or specified test data as prompted on the page. Click **Run Preview** to test the transformation rules.

   * If the page displays **DSL code compilation check failed**, it indicates an error in the transformation statement. You can refer to the error message on the page, fix the syntax issue in the specified line, and test the transformation rules again.

   * If you confirm that the data transformation results are correct, click **Create Write Processor**.

8. Select a write processor startup policy.

   In the pop\-up **Start immediately after task creation** dialog box, choose whether to enable the write processor immediately.

   * **Immediately enable**: Start the write processor immediately after configuration is complete.

   * **Enter pause mode**: Do not start the write processor after configuration is complete. You can manually start the task later as needed. For details, see [Manage write processors](https://docs.byteplus.com/docs/tls/Manage_data_processors).

   * **Cancel**: Cancel the creation of the write processor.

9. Associate a log topic.

   In the **Associate Log Topic** pop\-up window, select the log topic to associate, and click **OK**.
