---
title: "Managing index templates"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Managing_index_templates"
---

Index templates are used to automate the configuration of new indices. When you create indices that match specific naming patterns, Cloud Search automatically applies predefined configurations from templates. This ensures standardized index configurations, prevents manual configuration errors, and improves operation efficiency. This topic introduces how to manage index templates.

<span id="ZoqNGXCm"></span>
# Prerequisites


* A BytePlus account has been registered with real name authentication completed. For account registration and real name authentication, refer to [Create account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account#create-byteplus-account) and [Verify account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* Cross\-service access has been authorized to allow Cloud Search to access other services. For detailed steps, refer to [Cross-service Authorization](https://docs.byteplus.com/en/docs/cloudsearch/cross-service-authorization).

* Before managing index templates, create an Elasticsearch or OpenSearch instance. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).


<span id="6IyLvwKo"></span>
# Creating an index template


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the project and region where you want to create an index template.

3. In the left navigation bar, select **Index management**.

4. From the dropdown list, select the instance for which you want to manage index templates, enter the username and password, check **15 days license free** as needed, and then click **Authorized view index**.

5. On the **Index management** page, select the **Index template** tab, and click **Create index template**.

6. On the **Create index template** panel, configure the following parameters, and click **OK**.



|**Parameter** |**Description** |
|---|---|
|Template name |The name of the index template. The name must meet the following requirements:<br><br><br>   * Cannot start with a digit or underscore (_).<br><br>   * Contains 1 to 128 characters.<br><br>   * Contains only lowercase letters, digits, underscores (_), and hyphens (\-). |
|priority |The priority of the index template. If the name of an index matches multiple templates, the template with the highest priority is applied to the index. Recommended value range: 1~1000. |
|index mode |Separate multiple index patterns with commas (,) or line breaks. |
|Main sharding number |The number of primary shards for the index. |
|number of replicas |The number of replicas for the index. The number range is 1~10. |
|Translog (optional) |Select **asynchronous brush** or **synchronous swiping**. |
|refresh interval (optional) |Refresh interval for index templates. Unit: seconds. |
|compression method (optional) |Select **Speed first** or **Compression ratio priority**. |
|Index settings (Optional) |Configure index details. |


<span id="4V7cj7CF"></span>
# Editing an index template


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the project and region where you want to edit an index template.

3. In the left navigation bar, select **Index management**.

4. From the dropdown list, select the instance for which you want to manage index templates, enter the username and password, check **15 days license free** as needed, and then click **Authorized view index**.

5. On the **Index management** page, select the **Index template** tab, find the desired index template, and click **Edit** in the **Actions** column.

6. On the **Edit index template** panel, modify parameters as needed, and click **OK**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Editing index templates affects only subsequently created indices and does not affect indices that have been created. Therefore, if you want to change the structure of an existing index, you need to rebuild the index or use other strategies, such as transitioning with alias.</div>


<span id="agdUWUd3"></span>
# Deleting an index template


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the project and region where you want to delete an index template.

3. In the left navigation bar, select **Index management**.

4. From the dropdown list, select the instance for which you want to manage index templates, enter the username and password, check **15 days license free** as needed, and then click **Authorized view index**.

5. On the **Index management** page, select the **Index template** tab, find the desired index template, and click **Delete** in the **Actions** column.

6. In the dialog box that appears, confirm the index template information, enter the index template name, and then click **Delete**.
