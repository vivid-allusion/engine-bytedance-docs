---
title: "Importing Content data in Live Mode using API/SDK"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-importing_content_data_in_live_mode_using_api_sdk"
---

You can import your historical and incremental data through the APIs: [WriteUsers](https://docs.byteplus.com/en/recommend/reference/content_saas_writeusers), [WriteContents](https://docs.byteplus.com/en/recommend/reference/content_saas_writecontents), and [WriteUserEvents](https://docs.byteplus.com/en/recommend/reference/content_saas_writeuserevents). The data schema of the data sent through the API must match the schema defined in the BytePlus Recommend console.

<span id="3d2009f6"></span>
# Prerequisites

There are some prerequisites that you must fulfill before importing your trial data through the APIs:


* Have access to your BytePlus Recommend API keys. For more information on how to access your API keys, refer [here](https://docs.byteplus.com/en/byteplus-platform/docs/creating-an-accesskey).

* Requires 60\-100 days of data prepared.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The dates reflected in the Import data screen reflect the valid period for the required data. If you need to import data for a different time frame, whether more or less than the required period, reach out to the BytePlus Recommend team for assistance   </div>
   

<span id="508a3c5b"></span>
# Code samples

These are the code samples that you can refer to when importing data through APIs.


<Tabs>
<Tab zoneid="ZkjxtqE8Gh" title="WriteUsers">
<TabTitle>WriteUsers</TabTitle>

```Plain
curl --request POST \
     --url 'https://rec-api-sg1.recplusapi.com/ContentSaaS/WriteUsers' \
     --header 'accept: application/json' \
     --header 'content-type: application/json'
```



</Tab>
<Tab zoneid="CMl4C7f4gR" title="WriteContents">
<TabTitle>WriteContents</TabTitle>

```Plain
curl --request POST \
     --url 'https://rec-api-sg1.recplusapi.com/ContentSaaS/WriteContents' \
     --header 'accept: application/json' \
     --header 'content-type: application/json'
```



</Tab>
<Tab zoneid="hDToD0Xu8p" title="WriteUserEvents">
<TabTitle>WriteUserEvents</TabTitle>

```SQL
curl --request POST \
     --url 'https://rec-api-sg1.recplusapi.com/ContentSaaS/WriteUserEvents' \
     --header 'accept: application/json' \
     --header 'content-type: application/json'
```



</Tab>
</Tabs>


For more information on how to integrate your APIs, refer [here](https://docs.byteplus.com/en/recommend/docs/api_integration_dashboard).

<span id="fd7f1fb6"></span>
# Importing historical data to the console using API

Once you have prepared the files according to our requirements, you can proceed to import your historical data into the BytePlus Recommend console.

**To import data to the console using APIs:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Import Historical data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebae444b9b1d48d08a587661a89d4c8c~tplv-goo7wpa0wc-image.image) </span>

   The default import method is GCS.

3. Click the drop\-down menu and select **API/SDK**.

4. Click **Prepare resource for API import**.

   The BytePlus Recommend team will prepare our systems to receive your imported data.

5. Import using the APIs provided.

6. Once the importing has begun, click **Import data**.

   The data import process begins in the BytePlus Recommend console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41d51576c8e74c739e9f34045a9e78dd~tplv-goo7wpa0wc-image.image) </span>

7. Once your data validation report has been generated, click **Next**.

8. Resolve your imported data errors.

   For more information on resolving data errors, refer [here](https://docs.byteplus.com/recommend/docs/data_validation_reports).

   Your historical data import is completed.


<span id="707ce900"></span>
# Importing incremental data to the console using API

Once you have prepared the files according to our requirements, you can proceed to import your historical data into the BytePlus Recommend console.

**To import incremental data to the console using Amazon S3:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Validate Historical Data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76d7c5e6dbb049adbc2696084a1ebca8~tplv-goo7wpa0wc-image.image) </span>

3. Click **Next**.

   The Start incremental data import pop\-up window appears.

4. Click **Start**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After clicking Start, your historical data cannot be imported again.   </div>
   

   The Import Incremental data screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73dbe30769d64ff68c052a90ef545c55~tplv-goo7wpa0wc-image.image) </span>

   The default import method is GCS.

5. Click the drop\-down menu and select **API/SDK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/691272b3857b406e81c4aa30f86b0cb0~tplv-goo7wpa0wc-image.image) </span>

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
