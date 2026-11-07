---
title: "Debugging ETL rules through ETL Playground tool"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/debugging-ETL-rules-with-ETL-Playground-tool"
---

ETL Playground is a tool for verification of the accuracy of ETL rules. You can use this tool to verify the accuracy of data extraction, conversion, processing, and loading before changing the data, thereby reducing the impact and risks on the production environment. This topic describes how to verify the accuracy of the ETL rules you configured in the ETL Playground tool.

<span id=".5LyY5Yq_"></span>
## Advantages


* **Reduced risk**: In ETL Playground, you can safely experiment with and debug the ETL process, identify and fix potential errors and issues in a timely manner, thereby reducing the impact of these errors on actual production data and reducing risks.

* **Data Verification**: In ETL Playground, you can perform data Verification in ETL processes with complex data operations and numerical calculations to ensure the accuracy of the ETL process.

* **Performance optimization**: In ETL Playground, you can test different rules, view their impact on the ETL process, and find the optimal rule for them to improve the performance of the ETL process.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can test data on one table at most in a single time.

* You can verify up to 10 columns of data at a time, and add up to 10 rows of data for each column.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ETL Playground](https://console.byteplus.com/dts/region:dts+cn-guangzhou/etl-playground) tool.

2. In the **ETL rules** area on the **ETL Playground** page, refer to the DSL syntax to configure ETL rules. Refer to [DSL syntax](https://docs.byteplus.com/en/docs/DTS/dsl_syntax) for details about DSL syntax.

3. Click **Verification syntax** to test the accuracy of the ETL rules.

4. In the **Test data** area, set the table structure and data.

   * Table structure

      * On the **table structure** tab, set the **Database name** and **Table name**.

         ETL rules can only be verified on one table at a time.

      * Click **Add column** to set the **Column name** and **Data type**.

         * Column names cannot be duplicated.

         * You can verify up to 10 columns of data at a time, and add up to 10 rows of data for each column.

         * `String`, `binary`, `integer`, `float`, `decimal`, `bool`, `datetime`, `json`, and `unsigned integer` are supported for data type selection.

   * Data: On the **Data** tab, click **Add row** to set the row data information.

5. Click **debug** to confirm the **debug result**.
