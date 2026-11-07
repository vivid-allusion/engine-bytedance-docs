---
title: "Importing Retail data using API/SDK"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-importing_retail_data_in_live_mode_using_api_sdk"
---

You can import historical or incremental data in **Live Mode** through [WriteUsers](https://docs.byteplus.com/recommend/reference/retail_saas_writeusers), [WriteProducts](https://docs.byteplus.com/recommend/reference/retail_saas_writeproducts), and [WriteUserEvents](https://docs.byteplus.com/recommend/reference/retail_saas_writeuserevents) APIs. The data schema of the data sent through the API must match the schema defined in the BytePlus Recommend console.

<span id="44804019"></span>
# Prerequisites

There are some prerequisites that you must fulfill before importing your historical and incremental data through the APIs:


* Have access to your BytePlus Recommend API keys. For more information on how to access your API keys, refer [here](https://docs.byteplus.com/en/byteplus-platform/docs/creating-an-accesskey).

* Requires minimum 60\-100 days of data prepared.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The dates reflected in the Import data screen reflect the valid period for the required data. If you need to import data for a different time frame, whether more or less than the required period, reach out to the BytePlus Recommend team for assistance   </div>
   

<span id="41b76ce6"></span>
# Code samples

These are the code samples that you can refer to when importing data through APIs.


<Tabs>
<Tab zoneid="hM0D8UWbzD" title="WriteUser">
<TabTitle>WriteUser</TabTitle>

```Plain
curl --request POST 'rec-api-sg1.recplusapi.com/RetailSaaS/WriteUsers' \
     --header 'Request-Id: e92e0969-8250-4bb0-9f57-7c6366835b62' \
     --header 'Content-Type: application/json' \
     -d @request.json
```



</Tab>
<Tab zoneid="m20cVQtATH" title="WriteProduct">
<TabTitle>WriteProduct</TabTitle>

```Plain
curl --request POST 'rec-api-sg1.recplusapi.com/RetailSaaS/WriteProducts' \
     --header 'Request-Id: e92e0969-8250-4bb0-9f57-7c6366835b63' \
     --header 'Content-Type: application/json' \
     --d @request.json
```



</Tab>
<Tab zoneid="UGb3Jn1ex8" title="WriteUserEvent">
<TabTitle>WriteUserEvent</TabTitle>

```SQL
curl --request POST 'rec-api-sg1.recplusapi.com/RetailSaaS/WriteUserEvents' \
     --header 'Request-Id: e92e0969-8250-4bb0-9f57-7c6366835b62' \
     --header 'Content-Type: application/json' \
     -d @request.json
```



</Tab>
</Tabs>


For more information on how to integrate your APIs, refer [here](https://docs.byteplus.com/en/recommend/docs/api_integration_dashboard).

<span id="9ddc98d6"></span>
# Importing historical data to the console using API

Once you have prepared the files according to our requirements, you can proceed to import your historical data into the BytePlus Recommend console.

**To import data to the console using APIs:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Data screen appears.

3. Click **Import Data**.

   The Import Historical data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/427835ec7a5f4a539eec3877325e5c3d~tplv-goo7wpa0wc-image.image) </span>

   The default import method is GCS.

4. Click the drop\-down menu and select **API/SDK**.

5. Click **Prepare resource for API import**.

   The BytePlus Recommend team will prepare our systems to receive your imported data.

6. Import using the APIs provided.

7. Once the importing has begun, click **Import data**.

   The data import process begins in the BytePlus Recommend console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc16e2f1086c415aab2e83f5c3fea005~tplv-goo7wpa0wc-image.image) </span>

   For more information on the data import statuses, refer [here](https://docs.byteplus.com/recommend/docs/importing_retail_industry_data_overview#c45db7fe).

8. Once your data validation report has been generated, click **Next**.

9. Resolve your imported data errors.

   For more information on resolving data errors, refer [here](https://docs.byteplus.com/recommend/docs/data_validation_reports).

   Your historical data import is completed.


<span id="2b389b7d"></span>
# Importing incremental data to the console using API

Once you have prepared the files according to our requirements, you can proceed to import your incremental data into the BytePlus Recommend console.

**To import incremental data to the console using Amazon S3:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Validate Historical Data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6205448459ec44a7b4b8c0d35c0719ce~tplv-goo7wpa0wc-image.image) </span>

3. Click **Next**.

   The Start incremental data import pop\-up window appears.

4. Click **Start**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After clicking Start, your historical data cannot be imported again.   </div>
   

   The Import Incremental data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0247ad7323284f25851d507c3c92dc02~tplv-goo7wpa0wc-image.image) </span>

   The default import method is GCS.

5. Click the drop\-down menu and select **API/SDK**.

6. Click **Prepare resource for API import**.

   The BytePlus Recommend team will prepare our systems to receive your imported data.

7. Import using the APIs provided.

8. Once the importing has begun, click **Import data**.

   The data import process begins in the BytePlus Recommend console.

9. Once your data validation report has been generated, click **Next**.

10. Resolve your imported data errors.

   For more information on resolving data errors, refer [here](https://docs.byteplus.com/recommend/docs/data_validation_reports).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6580e114e7f14267b131641affd36c86~tplv-goo7wpa0wc-image.image) </span>

   Your incremental data import is completed.
