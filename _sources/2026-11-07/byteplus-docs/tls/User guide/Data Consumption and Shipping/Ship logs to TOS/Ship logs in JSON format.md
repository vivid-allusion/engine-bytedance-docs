---
title: "Ship logs in JSON format"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ship_log_in_json_format"
---

TLS supports shipping logs to TOS. This document uses JSON format as an example and describes the steps to configure log shipping.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* TLS has been enabled and log data has been successfully collected. For more details, see [Overview](https://docs.byteplus.com/docs/tls/getting_started_overview).

* TOS has been enabled , and a bucket has been created in the same region as the specified log topic. For more details, see [Creating bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* TLS needs to assume the ServiceRoleForTLS role to enable cross\-service access to other cloud resources. You must grant TLS permission to access and write to TOS resources.

   If you have not yet created the ServiceRoleForTLS role, TLS will guide you through the process when you create the shipping configuration. We recommend authorizing with the account. For details, see [Cross-service access authorization](https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access).


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1.  Log in to[ TLS console](https://console.byteplus.com/tls/).

2. Select the region where log service is located from the top navigation bar.

3. On the left navigation bar, select **Data processing** \> **Log shipping**.

4.  and then on the **Log shipping** page, click **Create TOS shipping configuration**.

5. On the **Create TOS shipping configuration** page, complete the following settings.

   1. Authorization settings.

      * If shipping to the same account, keep the default settings.

      * If shipping across accounts, configure authorization information.

         
         |Parameters |Description |
         |---|---|
         |Delivery target |Select **Deliver to another account**. |
         |IAM Role (TRN) |Enter the TRN for a custom role to grant permission for the shipping task to assume this role and deliver data across accounts to the TOS Bucket.<br><br>This custom role must have permission to deliver data.  |
         

   2. Configure basic information.

      
      |Parameters |Description |
      |---|---|
      |Configuration name |Name of the log shipping configuration. |
      |Source project |Select the project where the data source is located from the dropdown list. |
      |Source topic |Select the topic where the data source is located from the dropdown list. |
      

   3. Configure log shipping target information.

      
      |Parameters |Description |
      |---|---|
      |Target bucket |Select a TOS bucket, which must be in the same region as the source topic.<br><br>If you do not have a suitable bucket, you can follow the prompts on the page to create a new one. |
      |Shipping directory |The top\-level directory name of the bucket. All log data shipped according to this configuration will be shipped to this directory. |
      |Shard format |Subdirectory naming format in the bucket. TLS dynamically generates subdirectories in the specified shipping directory based on the creation time of the shipping configuration. The subdirectory naming format supports [strftime](http://man7.org/linux/man-pages/man3/strptime.3.html) syntax. |
      

      The following shows examples of shard formats and corresponding TOS bucket directory structures:

      
      |Shard format values |Corresponding TOS bucket directory structure (using 2022/06/30/14/00 as an example) |
      |---|---|
      |%Y/%m/%d/%H/%M (default value) |tos://bucket\-name/top\-level\-directory\-name/2022/06/30/14/00/ |
      |%Y%m%d%H |tos://bucket\-name/top\-level\-directory\-name/2022063014/ |
      |%Y%m%d |tos://bucket\-name/top\-level\-directory\-name/20220630/ |
      |ds=%Y%m%d/%H |tos://bucket\-name/top\-level\-directory\-name/ds=20220630/14/ |
      |year=%Y/mon=%m/day=%d/log_%H%M |tos://bucket\-name/top\-level\-directory\-name/year=2022/mon=06/day=30/log_1400/ |
      



&nbsp;

   4. (Optional) Configure advanced settings for log shipping target.

      
      |Parameters |Description |
      |---|---|
      |Set the shard based on the value |Defines the naming format for subdirectories in the bucket. This directory will appear as either the parent or child of the time shard subdirectory.<br><br>Disabled by default. After enabling, select the level for this directory and set the corresponding key and value regular expressions.<br><br><br>* Key (required): Select the key used for shard shipping of the value.<br><br>* Value regular expression (optional):<br><br>   * Set the regular expression to extract the value of the corresponding key. The extracted value will serve as the name of the subdirectory in the bucket.<br><br>   * If not set, all fields for the corresponding key will be automatically extracted, and each field will be used as a subdirectory name in the bucket.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This may generate too many small files. Up to 100 shards are supported. Extra files will be shipped to the subdirectory named <code>others</code>. Configure with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the configured key does not exist or regular expression extraction fails, the setting will not take effect.</div><br> |
      

      Example:

      * Original log: `{"name":"Li Si","address":"Guangdong Province, Shenzhen XXX Science Park","phone":"13xxxxxx321"}`

      * Configuration example:

         <div style="text-align: center">
         <img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bceb7160e46d45d4985c56b9df5f2c79" width="738px" />         </div>
         

      * Shipping result:

         In the TOS destination bucket, the data will be shipped to the corresponding directory based on whether the regular expression `(.*?province)` is configured.

         * Set regular expression: `tos://if-tls-test/No1-test/Guangdong Province/2022/06/30/14/00/`.

         * No regular expression configured: `tos://if-tls-test/No1-test/Guangdong Province Shenzhen xxx Technology Park/2022/06/30/14/00/`.

   5. Configure log shipping formats.

      
      |Parameters |Description |
      |---|---|
      |Compression type |Log data can be compressed using a specified compression format before being shipped to object storage TOS. This can help to save read traffic costs. Supports uncompressed, snappy, gzip, and lz4. |
      |Shipping format |The format in which data is stored after being shipped to TOS.<br><br>In this topic, JSON format is used as an example. |
      |Shipping fields |When shipping in JSON format, all fields are included, including metadata fields such as `__source__`, which are added by TLS for each log by default. |
      

   6. Configure shipping rules.

      Shipping rules specify the trigger conditions for log shipping actions. After you create the shipping configuration, TLS continues to record the interval since the last shipping. When the specified interval is reached, TLS packages and ships log data from each shard to TOS separately. If the volume of new data in a shard exceeds the specified file size for shipping, TLS automatically splits the files to meet the size requirement.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Each delivered file corresponds to an object in TOS.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The delivered file size refers to the volume of original data before compression. If compression is enabled, the files saved in TOS after shipping will be smaller than the delivered file size, reducing storage costs.      </div>
      

      
      |Parameters |Description |
      |---|---|
      |Delivered file size |The original file size to be delivered for each shard, which means the uncompressed log file size. The unit is MiB, and the value range is 5–256. |
      |Time interval of log shipping |The interval between log shipping actions. The unit is seconds. The value ranges from 60 to 900. |
      |Shipping time range  |Deliver log data within the specified time range.<br><br><br>* Start time: The earliest write time of the log data to be delivered. The default start time is the current moment. You can choose a historical time, which means the log data that collected before shipping rule was created can also be shipped to TOS.<br><br>* End time: The latest write time of the log data to be shipped. TLS does not ship deliver log data collected after this time. If the end time is left empty, the most recent log data will continue to be shipped.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">Once the shipping configuration is created, you can not modify the shipping time range.</div><br> |
      

   7. Click **create**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

Once the shipping configuration is created successfully, TLS automatically sets the task status to enabled and triggers a log shipping task. You can view details such as the shipping configuration name on the log shipping page. For more information, see [View shipping configuration and task details](https://docs.byteplus.com/docs/tls/manage_shipping_rules_tos#.5p-l55yL5oqV6YCS6YWN572u5ZKM5Lu75Yqh6K-m5oOF); you can also view shipped log data directly in the object storage console.
