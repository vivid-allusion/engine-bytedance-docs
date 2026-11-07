---
title: "Index configuration"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/index-config_en-us"
---

For CDN logs delivered to BytePlus Log Service (TLS), you can configure indexes to customize log management and enable flexible queries. This guide provides the steps to locate and modify the index configuration for a specific log topic.

The index configuration determines which fields are indexed by TLS and how they are indexed. In CDN, you can configure indexes for a log topic as needed to achieve customized log management. The steps are as follows:


1. In the list of real\-time log delivery tasks, find the task for which you want to modify the index configuration.

2. From the task configuration, identify the log project, its region, and the log topic where the logs are stored.

3. In the **Actions** column, click **Query Logs**.

4. At the top of the Log Service page that opens, select the region where the log project is located, and then click **Query and analysis** on the left side of the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/571741db015746a6aa65054fe3df08bf~tplv-goo7wpa0wc-image.image) </span>

5. On the left side of the **Query and analysis** page, find and open the corresponding log topic.

6. On the log topic details page, click **Index configuration**.

7. Configure the index according to the [Configuration Instructions](https://docs.byteplus.com/docs/byteplus-cdn/index-config_en-us#4c07c902).

8. After completing the configuration, click **OK**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1257db0493874f5ebf648d6a2272479f~tplv-goo7wpa0wc-image.image) </span>

<span id="4c07c902"></span>
## Configuration Instructions


|Configuration |Description |
|---|---|
|Field name |Represents a log field. |
|Field type |Represents the data type of the field. |
|Field configuration |Represents how BytePlus TLS indexes the field. The log service provides the following configurations:<br><br><br>* Case Sensitive: Indicates whether the field name is case\-sensitive.<br><br>* Contains Chinese: Indicates whether the field value contains Chinese characters. If you enable this option, the log service tokenizes the field value using Chinese word segmentation rules. For example, if a field's value is `msg:"文件 sample.png 打开失败"`. If **Contains Chinese** is disabled, a query must match the entire field value (e.g., `msg:"文件 sample.png 打开失败"`); a partial query like `msg:"打开"` will fail. If enabled, the partial query `msg:"打开"` can retrieve the log.<br><br>* Delimiter: Indicates which character the log service uses to tokenize the field value. The purpose of tokenization is to facilitate retrieval. For example, if a field's value is `numbers:"1\|2\|3"` and you specify the delimiter as `\|`, the query statement `numbers:"1"` can retrieve this log. If you specify the delimiter as `,`, the query statement `numbers:"1"` will not retrieve this log.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The <strong>Contains Chinese</strong> and <strong>Delimiter</strong> options are mutually exclusive.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only text type and json type fields have <strong>Contains Chinese</strong> and <strong>Delimiter</strong> configurations.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, there are the following limitations:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If <strong>Enable analytics</strong> is enabled for a field, the <strong>Contains Chinese</strong> and <strong>Delimiter</strong> options for that field become unavailable.</div><br> |
|Enable analytics |Indicates whether the field can be specified in analysis statements. The format of a query statement is `<query statement>\|<analysis statement>`. If you do not want a field to be used in analysis statements, you can disable the **Enable analytics** option for it.<br><br>Note that regardless of whether **Enable analytics** is turned on, the field can always be specified in query statements. For example, if you set the **Enable analytics** of the `ds_http_status` field to off. At this point, you cannot run the following query statement:<br><br><br>* `ds_http_status:>=400 \| select ds_http_status,count(*) AS PV group by ds_http_status`<br><br><br>However, you can still run the following query statement:<br><br><br>* `ds_http_status:>=400` |
|Actions |To remove the index configuration for a field, click **Delete**. |


For other index configurations on this page, such as full\-text indexing, see [the TLS Documentation](https://docs.byteplus.com/en/docs/tls/Configure-indexes-2).
