---
title: "Importing Retail data in Trial Mode using API/SDK"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-importing_retail_data_using_api_sdk"
---

You can import trial data through the APIs: [WriteUsers](https://docs.byteplus.com/recommend/reference/retail_saas_writeusers), [WriteProducts](https://docs.byteplus.com/recommend/reference/retail_saas_writeproducts), and [WriteUserEvents](https://docs.byteplus.com/recommend/reference/retail_saas_writeuserevents). The data schema of the data sent through the API must match the schema defined in the BytePlus Recommend console.

<span id="c74649b8"></span>
# Prerequisites

There are some prerequisites that you must fulfill before importing your trial data through the APIs:


* Have access to your BytePlus Recommend API keys. For more information on how to access your API keys, refer [here](https://docs.byteplus.com/en/byteplus-platform/docs/creating-an-accesskey).

* Requires 1\-2 weeks of data prepared.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The dates reflected in the Import data screen reflect the valid period for the required data. If you need to import data for a different time frame, whether more or less than the required period, reach out to the BytePlus Recommend team for assistance   </div>
   

<span id="de20eceb"></span>
# Code samples

These are the code samples that you can refer to when importing data through APIs.


<Tabs>
<Tab zoneid="Gxu99TAzMu" title="WriteUsers">
<TabTitle>WriteUsers</TabTitle>

```Plain
curl --request POST 'rec-api-sg1.recplusapi.com/RetailSaaS/WriteUsers' \
     --header 'Request-Id: e92e0969-8250-4bb0-9f57-7c6366835b62' \
     --header 'Content-Type: application/json' \
     -d @request.json
```



</Tab>
<Tab zoneid="l9DASkXbPC" title="WriteProducts">
<TabTitle>WriteProducts</TabTitle>

```Plain
curl --request POST 'rec-api-sg1.recplusapi.com/RetailSaaS/WriteProducts' \
     --header 'Request-Id: e92e0969-8250-4bb0-9f57-7c6366835b63' \
     --header 'Content-Type: application/json' \
     --d @request.json
```



</Tab>
<Tab zoneid="HLwlvldQV8" title="WriteUserEvents">
<TabTitle>WriteUserEvents</TabTitle>

```SQL
curl --request POST 'rec-api-sg1.recplusapi.com/RetailSaaS/WriteUserEvents' \
     --header 'Request-Id: e92e0969-8250-4bb0-9f57-7c6366835b62' \
     --header 'Content-Type: application/json' \
     -d @request.json
```



</Tab>
</Tabs>


For more information on how to integrate your APIs, refer [here](https://docs.byteplus.com/en/recommend/docs/api_integration_dashboard).

<span id="66fff1b5"></span>
# Importing data to the console using API

Once you have prepared the files according to our requirements, you can proceed to import the trial data into the BytePlus Recommend console.

**To import data to the console using APIs:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Configure screen appears.

3. Click **Next**.

   The Import screen appears.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bc50db3c4b3457bb22e318180740cbc~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   The default import method is GCS.

4. Click the drop\-down menu and select **API/SDK**.

5. Click **Prepare resource**.

   The BytePlus Recommend team will prepare our systems to receive your imported data.

6. Import using the APIs provided.

7. Once the importing has begun, click **Import data**.

   The data import process begins in the BytePlus Recommend console.
