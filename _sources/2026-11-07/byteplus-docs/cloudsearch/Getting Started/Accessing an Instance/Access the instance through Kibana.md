---
title: "Access the instance through Kibana"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/accessing-by-Kibana"
---

This topic describes the background information and procedure for accessing the instance through Kibana.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

After the Cloud Search instance is created, you can connect to the ES instance to start using it, such as defining index data, importing data, and searching data. You can access the instance through the following methods:


* [Access the instance through Kibana in the management console](https://docs.byteplus.com/docs/cloudsearch/accessing-by-Kibana)

* [Access the instance via Elasticsearch RESTful API](https://docs.byteplus.com/docs/cloudsearch/accessing-by-API)

* [Access the instance using clients in various programming languages](https://docs.byteplus.com/docs/cloudsearch/accessing-by-client)


Cloud Search includes a Kibana module where you can visit the Kibana page for the instance to perform data visualization, query analysis, and data management. You can use this tutorial to quickly get started with Kibana.

<span id=".5q2l6aqk5LiA77ya55m75b2VIEtpYmFuYQ=="></span>
## Step 1: Log in to Kibana

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, to ensure security, Kibana only allows access from internal network addresses. To access it via a public network, follow the steps below to obtain a public network address.</div>



1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. Enable public network access for the Kibana node. For detailed steps, see [Configure Kibana/Dashboards public network access](https://docs.byteplus.com/docs/cloudsearch/enabling-public-access-tool).

3. After enabling public network access, click the Kibana public network access link.

4. Enter the username and password on the Kibana login page, then click **Log in** to sign in to Kibana.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The username is admin, and the password is the one you set when creating the instance. If you forget the login password, you can reset it. For detailed steps, see <a href="https://docs.byteplus.com/docs/cloudsearch/resetting-password">Reset password</a>.   </div>
   

5. In the Kibana left menu, click **Dev Tools** to open the developer tools page and access the instance within Kibana.


<span id=".5q2l6aqk5LqM77ya5re75Yqg57Si5byV5Y-K5paH5qGj"></span>
## Step two: add index and documentation

After logging into the Kibana page, if this is your first time and the instance has not stored the index data you defined, the page will prompt you to configure the index. The detailed steps are as follows.

You can send various operation requests to the instance through the console. The following example uses data storage operations to demonstrate how to operate the instance and store data through the console.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This article uses Elasticsearch instance version 7.10.2 as an example; some commands are not supported in lower versions.</div>


<span id=".5a6a5LmJ57Si5byV55qEIG1hcHBpbmc="></span>
### Define index mapping

Create an index named `customer` and define detailed fields and type information as follows. Among them, `level` is an object type containing second\-level field information.

```SQL
PUT  /customer 
{  
   "mappings":{
        "properties":  { 
            "name":  {"type": "keyword"},
            "address": {"type": "keyword"},
            "city":{ "type": "keyword" },
            "age":{ "type": "integer" },
            "birthday":{"type": "date"},
            "level":{ 
              "properties": {
                "viplevel":{ "type": "integer" },
                "viptype":{ "type": "keyword" }
              }
            }
        }  
   }
}
```


<span id=".5re75Yqg5Y2V5Liq5paH5qGj"></span>
### Add a single document

Add a document with `id` 1 to the index.

```SQL
POST  /customer/_doc/1
{
  "name": "张三",
  "address":"四川省成都市武侯区",
  "city":"成都",
  "age":28,
  "birthday":"1993-08-30",
  "level": {
    "viplevel":3,
    "viptype":"黄金会员"
  }
}
```


<span id=".5re75Yqg5aSa5Liq5paH5qGj"></span>
### Add multiple documents

Batch add documents to the index.

```SQL
POST _bulk
{"index" : { "_index": "customer","_id":2} }
{"name":"李四","address":"北京市海淀区","city":"北京","age":"23","birthday":"1998-01-01","level":{"viplevel":3,"viptype":"黄金会员"}}
{"index" : { "_index": "customer","_id":3} }
{"name":"王五","address":"浙江省内杭州市滨江区","city":"杭州","age":"30","birthday":"1991-05-05","level":{"viplevel":5,"viptype":"钻石会员"}}
```


<span id=".5p-l6K-i5Y2V5Liq5paH5qGj"></span>
### Query a single document

Query the document with the specified `id`.

```SQL
GET /customer/_doc/1
```


<span id=".5p-l6K-i5aSa5Liq5paH5qGj"></span>
### Query all documents

Query all documents in the index.

```SQL
GET /customer/_search
```


<span id=".5q2l6aqk5LiJ77ya6K6_6Zeu57Si5byV"></span>
## Step three: Access the index

<span id=".6YWN572uIEtpYmFuYSDorr_pl67ntKLlvJU="></span>
### Configure Kibana to access the index

To use Kibana, configure at least one matching index.

Select the **Stack Management \> Index patterns \> Create index pattern** screen, enter the index `customer` created in the previous step, then click **Next step** to continue.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_66330e8a5ca3fc21d9a397eabe1ddbbb.png) </span>


* **Configure the time filter field**: used to filter data in the index by time. If the index has no time field, you can choose not to use the time filter feature. Click **Create index pattern** to create an index pattern.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_af69c49b3e042c90886a18aec862fd7c.png) </span>

* **View the fields corresponding to the index**

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff68db8087a7cb2b344e957a22e3c61c.png) </span>

* **View documents**: click **Discover** in the upper left menu to view documents added under this index.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d437bbf103ad104c357088484219a6ae.png) </span>


<span id=".5Y-v6KeG5YyW5p-l6K-i5YiG5p6Q"></span>
### Visualize query analysis

Kibana can visualize and analyze data. You can configure various charts for data analysis.

For example, count different viplevels under the `customer` index mentioned above.


1. Click **Visualize** in the upper left menu, then click **Create new visualization**.

2. Select the appropriate visualization type in the **New Visualization** dialog.

   Select **pie** here to see the categories and proportions of viplevel values.

3. Select the index to analyze.

4. Create a bucket aggregation to the right of the pie chart, using **Terms** multi\-value aggregation to query and analyze index documents.

   1. In the **Buckets** area, click **Add** and choose **Split slices**.

   2. Select aggregation as **Terms**, analysis field as **level.viplevel**, metric as **Count**, then click **Update**.

      You can now view the categories and proportions of viplevel values on the pie chart.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4b46beaa2a173d8590e777b722ea3067.png) </span>

5. Click the **Save** button at the top right of the page, then set the name and description of the visualization and save it.
