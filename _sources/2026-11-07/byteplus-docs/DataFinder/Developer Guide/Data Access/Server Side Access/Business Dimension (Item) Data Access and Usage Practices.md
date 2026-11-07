---
title: "Business Dimension (Item) Data Access and Usage Practices"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Business_Dimension_Item_Data_Access_and_Usage_Practices"
---

The following takes a specific business scenario as an example to introduce the reporting practice of business dimension (item) data.

<span id="d550bb01"></span>
# Background information: Item creation, access and use process key points

When creating and reporting using business dimension (Item) data on the DataFinder, the general operational process is as follows. You can first understand the process points introduced to you below, and then refer to the detailed examples below to understand the specific operation steps.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can refer to the following process guide to choose a more convenient access and use process according to the current use environment. If you are unsure of the current environment type, see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


<span id="98630721"></span>
## SaaS\-cloud native environment


1. You need to first report the dimensions according to the actual needs, in the DataFinder console, data management \> metadata management \> business dimensions, page to create business dimensions, and define its properties, the business dimensions to be reported and its properties into the DataFinder metadata, see for details [Create/edit business dimensions](https://docs.byteplus.com/docs/DataFinder/Item_Business_Dimension#8128143e).

2. After the business dimension and attributes are entered into the metadata, you can start reporting the attributes of the business dimension. Currently, it supports uploading the attributes of the business dimension directly through files, and also supports reporting through code.

   * File upload: This method is only supported by SaaS\-cloud native environments, see [Business Dimension (Item) Data Access (Local File Upload)](https://docs.byteplus.com/docs/DataFinder/Business_Dimension_Item_Data_Access_Local_File_Upload) for details.

   * Code reporting: SaaS \- cloud native environment See [HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API).

3. The created business dimension needs to be associated with a user behavior event before it can be used for subsequent analysis, so you need to associate the Item with the reported event before the event is reported. Event association can be reported in two ways through interface configuration and code:

   * (Recommended) Interface configuration: This method is only supported by SaaS\-cloud native environment. It is recommended to use this method for association. The configuration is more flexible. Please refer to the details [Create/edit business dimensions](https://docs.byteplus.com/docs/DataFinder/Item_Business_Dimension#8128143e).

   * Code reporting: Code reporting needs to add __items field (format JSON string, containing item name and corresponding ID list) to the params of the event. SaaS \- Cloud Native Environment See [HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API).

4. After completing the above process, you can perform business dimension analysis on the Analytics Tools \> Advanced Analytics \> Business Dimension Analysis page of the DataFinder console after the data is reported, and the event introduces these dimensions through the ID of the associated item, see details [Item Analysis](https://docs.byteplus.com/docs/DataFinder/Item_Analysis).


<span id="47353905"></span>
# Sample business data

In this example, the example account is the account of X<ins>iaoyang</ins> making the purchase event in the App, the purchase product name is ++[❤️ cost\-effective recommendation ❤️] day selection 5 15.6 inches high\-performance game book, notebook computer ++, the number of purchased goods is ++3 ++, the total price is ++20,000 ++, the consignee is ++Zhang San ++.

The business dimension table and event tracking requirements covered in the example are as follows:


* <ins>Dimension 1: Commodities</ins>

   
   |product_id |product_cn |second_grad |amall_product_name |third_garde |
   |---|---|---|---|---|
   |C01 |90NRM200 |Heaven's Choice |<ins>[❤️ cost\-effective recommendation ❤️] Tianxuan 5 15.6\-inch high\-performance game book, laptop</ins> |Skypick 5 |
   |i01 |90pad1233 |Mini pc |<ins>[❤️ king of cost performance ❤️] Xiaomi pad</ins> |minipc |
   |t01 |90phone678 |outsourcing |<ins>[❤️ students must choose ❤️] oppo photo</ins> |purchase |
   

* <ins>Dimension Table 2: Consignee</ins>

   
   |account_id (account id) |consignee__name |nick_name |Address |phoneNum (Telephone) |
   |---|---|---|---|---|
   |001 |Lamb |Zhang San |Luoyang, Henan |156797759081 |
   |002 |Twilight Dawn |Zhang Wu |Shijiazhuang, Hebei |156797222281 |
   |003 |Evergreen |Li Si |Beijing Haidian |157766568659 |
   

* <ins>Tracking event requirements</ins>

   
   |event name |event time |event properties |Other device information |
   |---|---|---|---|
   |pay |Current time |quantity |ignore |
   |||consignee ||
   |||Product name ||
   


<span id="aeafb8c5"></span>
# Item Data Access Practice

<span id="e1108911"></span>
## Step1: Create a business dimension table

See the activity details for creating a business dimension table [Item (Business Dimension)](https://docs.byteplus.com/docs/DataFinder/Item_Business_Dimension), the configuration points are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d3e9373540e400c9e05698bb98ce6c6~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2c097cc80e2473cb94e0ee712698101~tplv-goo7wpa0wc-image.image) </span>

**The actual creation effect is as shown in the figure:** 


* Product dimension

* consignee dimension table


<span id="f2c6ea7d"></span>
## Step2: Report dimension table attribute data

There are two ways to report, you can choose one according to your needs


* File upload: [Business Dimension (Item) Data Access (Local File Upload)](https://docs.byteplus.com/docs/DataFinder/Business_Dimension_Item_Data_Access_Local_File_Upload)

* Code reporting: See [HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API).

   ```SQL
   curl --location 'report address' \
   --header 'Content-Type: application/json' \
   --header 'X-MCS-AppKey: appkey' \
   --data '{
       "user": {
           "user_unique_id": "__rangers"
       },
       "events": [
           {
               "event": "__item_set",
               "local_time_ms": 1721044941000,
               "params": "{\"item_name\":\"product\",\"item_id\":\"C01\",\"product_cn\": \"90NRM200\",\"product_name\":\"[❤️ cost-effective recommendation ❤️] Tianxuan 5 15.6-inch high-performance game book, laptop\",\"third_garde\": \"Skypick 5\"}"
           }
       ],
       "header": {
           "app_name": "AAA"
       }
   }'
   ```
   


<span id="39f31886"></span>
## Step3: Incident reporting

See [HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API).

```SQL
curl --location 'report address' \
--header 'Content-Type: application/json' \
--header 'X-MCS-AppKey: appkey' \
--data '{
    "user": {
        "user_unique_id": "001"
    },
    "header": {
        "app_name": "test",
        "app_package": "com.ss.android.article.news",
        "app_version": "5.1.3",
        "custom":{
             "__is_history": "true"
              }
    },
    "events": [
        {
            "event": "lhy_test",
            "params": "{\"user_is_login\":1,\"num\":3，\"color\":\"C01\"，\"consignee\":\"\"001}",
            "local_time_ms": 1733395152000
        }
    ]
}'
```


<span id="bd9717b1"></span>
## Step4: reporting events and dimension table bindings

See [HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API).

```SQL
...
"event": "lhy_test",
"params": {
    "__items": "[{\"product\":[{\"id\":\"C01\"}]},{\"consignee\":[{\"id\":\"001\"}]}]",
    ...
},
```
