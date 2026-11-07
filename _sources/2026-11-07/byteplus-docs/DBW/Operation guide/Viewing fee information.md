---
title: "Viewing fee information"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Viewing_fee_information"
---

This topic describes how to view the fees incurred when using Database Workshop (DBW).

<span id="L8HsjL8c"></span>
## Precautions


* IAM users do not have bill viewing permissions by default. To view fee details, IAM users must have `DbwFullAccess`, `DBWDASFullAccess`, or `DBWDASReadOnlyAccess` permissions. For detailed steps, refer to [Sub-account permission management](https://docs.byteplus.com/en/docs/DBW/managing-permissions-of-an-sub-account?lang=zh).

* SQL insights and auditing statistics are stored in DBW instances. Audit type includes database audit for Cache for Redis V1, database audit for Document Database for MongoDB V1, database audit for RDS for MySQL V2, database audit for veDB for MySQL V2, and dDatabase audit for RDS for PostgreSQL V2.


<span id="azXB8S05"></span>
## Region


|**Region** ||**RegionId** |
|---|---|---|
|China |China (Shanghai) |cn\-shanghai |
||China (Beijing) |cn\-beijing |
||China (Guangzhou) |cn\-guangzhou |
||China (Hong Kong) |cn\-hongkong |
|Overseas |Asia Pacific (Johor) |ap\-southeast\-1 |
||Asia Pacific (Jakarta) |ap\-southeast\-3 |


<span id="HZHYx7dH"></span>
## Billing

DBW currently only supports pay\-as\-you\-go billing, which is postpaid. For more billing information, see [Billing overview](https://docs.byteplus.com/en/docs/DBW/billing-description?lang=zh).

<span id="x2wdnN7r"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, click Fee information.

3. On the **Fee information** page, view the following information.

   * **SQL insights and auditing**: This section displays the count of all instances with audit data stored in DBW.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">For instances with audit data stored in DBW, the audit type includes database audit for Cache for Redis V1, database audit for Document Database for MongoDB V1, database audit for RDS for MySQL V2, database audit for veDB for MySQL V2, and database audit for RDS for PostgreSQL V2.      </div>
      

   * **Usage statistics of various types**: This area displays traffic usage for all instances, including **index standard storage**, **log standard storage**, **index traffic**, **log traffic**, and **aggregate analysis volume**.

   * Instance billing information: This area displays details including **Instance name/ID**, **billing instance ID**, **Database type**, **instance audit**, **SQL insight**, **Index storage \- Cumulative**, **Log storage \- Cumulative**, **Index traffic \- of the day**, **Log traffic \- same day**, **Aggregate analysis volume \- of the day**, **Owning project**, and **Tag**. In this area, you can also view the target instance's **Usage trend** and **Billing information**, as detailed below:

      * Usage trend: Click **Usage trend** in the **Actions** column of the target instance. On the **Usage trend** control panel, you can view the instance's **Storage usage**, **Log and index traffic**, and **Total aggregation analysis volume** over the past 24 hours. Actual usage information is subject to the billing details.

      * Billing information: Click **Check bill** in the **Actions** column to navigate to the billing details page in the Billing platform, where you can view all billing information under the current account.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The <strong>billing instance ID</strong> corresponds to the instance ID in the <strong>billing information</strong> page's <strong>billing details</strong> tab on the billing platform, allowing you to filter and view more billing details.      </div>
      

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><strong>Index storage \- Cumulative</strong> and <strong>Log storage \- Cumulative</strong> display the current non\-expired storage information.      </div>
      

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The data for <strong>Index traffic \- of the day</strong>, <strong>Log traffic \- same day</strong>, and <strong>Aggregate analysis volume \- of the day</strong> reflect traffic information from the past 1 hour.      </div>
      

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In this area, you can also bind or add tags to the instance. Tags help allocate costs to corresponding cost units for refined cost management and internal settlements. Click the tag icon in the <strong>Tag</strong> column of the target instance. In the <strong>Edit tag</strong> dialog box, select or enter a new tag key and value to add a tag to the instance. The rules for tag key\-value pairs are as follows:      </div>
      

               * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Key      </div>
      

                  * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Supports any language, characters, numbers, spaces, or symbols (_.:/=+\-@).      </div>
      

                  * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Case\-sensitive, and the length is 1 \- 128 characters.      </div>
      

                  * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In UTF\-8 encoded Unicode format.      </div>
      

                  * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Keys cannot start with any form of volc:, such as Volc: or VOLC:.      </div>
      

               * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">(Optional) value      </div>
      

                  * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Supports any language, character, digit, space, or symbol (_.:/=+\-@).      </div>
      

                  * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Case\-sensitive, and the length is 0–256 characters.      </div>
      

                  * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Use the Unicode format encoded with UTF\-8.      </div>
      

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">A maximum of 20 tags can be associated with a task in a single operation, and a single task can have up to 50 tags. For a single resource, tag keys must be unique, and each tag key can have only one Value.          </div>
