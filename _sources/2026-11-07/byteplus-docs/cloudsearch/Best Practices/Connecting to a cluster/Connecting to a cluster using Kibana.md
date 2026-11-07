---
title: "Connecting to a cluster using Kibana"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/connecting-cluster-Kibana"
---

The system deploys a Kibana node as the data visualization tool when you create a Cloud Search instance. You can use this tool to view and interact with index data and visually display and analyze data in charts. This topic describes how to connect to a Cloud Search instance by using Kibana and provides examples of simple operations.

<span id="3d2d0512"></span>
## Before you begin

Enable internet\-facing access to Kibana if you want to access Kibana by using its public endpoint. For more information, refer to [Enabling public network access to Kibana](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access-tool).

Internal access is enabled for Kibana by default. You do not need to manually enable it.

<span id="47206c1f"></span>
## Logging on to Kibana by using the public endpoint


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of the target instance.

3. Go to the Kibana logon page by using one of the following methods:

   * On the **Instances** page, find the instance and click **Kibana** or **Dashboards** in the **Actions** column.

   * In **Instance management \>**  **Visulization configuration**, click the public network access address.

4. On the Kibana logon page, type the username and password, then click **Log In**.

   The username is admin, and the password is the one you set when creating the instance. If you forgot your logon password, reset the password on the **Instance information** page. For more information, refer to [Resetting the instance password](https://docs.byteplus.com/en/docs/cloudsearch/resetting-password).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/826ab6d2df5f4888a0e6b5a2db4f04e0~tplv-goo7wpa0wc-image.image) </span>


<span id="2ea17e56"></span>
## Managing indices through Kibana

On the Kibana page, go to **Management \> Dev Tools**. You can define indices, write documents, and query data through Kibana.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The following commands are run on a Cloud Search instance with version <strong><code>7.10.2</code></strong> because some commands are not supported in earlier versions.</div>


<span id="9b30d8b7"></span>
### Defining the mapping of an index

Create an index named `customer`, and define the detailed fields and their types for the index. Where, `level` specifies the object type, which contains level\-2 field information.

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


<span id="b91dd4ac"></span>
### Adding a single document

Add a document whose `id` is 1 to the index.

```SQL
POST  /customer/_doc/1
{
  "name": "Alice",
  "address":"Wuhou District, Chengdu City, Sichuan Province",
  "city":"Chengdu",
  "age":28,
  "birthday":"1993-08-30",
  "level": {
    "viplevel":3,
    "viptype":"Premium VIP"
  }
}
```


<span id="b029f725"></span>
### Adding multiple documents

Add multiple documents to the index at a time.

```SQL
POST _bulk
{"index" : { "_index": "customer","_id":2} }
{"name":"Tom","address":"Haidian District","city":"Beijing","age":"23","birthday":"1998-01-01","level":{"viplevel":3,"viptype":"Premium VIP"}}
{"index" : { "_index": "customer","_id":3} }
{"name":"Joe","address":"Binjiang District, Hangzhou City, Zhejiang Province","city":"Hangzhou","age":"30","birthday":"1991-05-05","level":{"viplevel":5,"viptype":"Diamond VIP"}}
```


<span id="5d6a963c"></span>
### Querying a single document

Query a document with a specified `id`.

```SQL
GET /customer/_doc/1
```


<span id="a3bc8769"></span>
### Querying all documents

Query all the documents in the index.

```SQL
GET /customer/_search
```
