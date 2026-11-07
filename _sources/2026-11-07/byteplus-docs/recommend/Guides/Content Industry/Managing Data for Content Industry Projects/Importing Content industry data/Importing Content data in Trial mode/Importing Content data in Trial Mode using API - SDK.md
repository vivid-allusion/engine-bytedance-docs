---
title: "Importing Content data in Trial Mode using API/SDK"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-importing_content_data_in_trial_mode_using_api_sdk"
---

You can import trial data through the APIs: [WriteUsers](https://docs.byteplus.com/en/recommend/reference/content_saas_writeusers), [WriteContents](https://docs.byteplus.com/en/recommend/reference/content_saas_writecontents), and [WriteUserEvents](https://docs.byteplus.com/en/recommend/reference/content_saas_writeuserevents). The data schema of the data sent through the API must match the schema defined in the BytePlus Recommend console.

<span id="8cb1d5f9"></span>
# Prerequisites

There are some prerequisites that you must fulfill before importing your trial data through the APIs:


* Have access to your BytePlus Recommend API keys. For more information on how to access your API keys, refer [here](https://docs.byteplus.com/en/byteplus-platform/docs/creating-an-accesskey).

* Requires 1\-2 weeks of data prepared.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The dates reflected in the Import data screen reflect the valid period for the required data. If you need to import data for a different time frame, whether more or less than the required period, reach out to the BytePlus Recommend team for assistance   </div>
   

<span id="891e8e0a"></span>
# Code samples

These are the code samples that you can refer to when importing data through APIs.


<Tabs>
<Tab zoneid="PZYI1Cywyd" title="WriteUsers">
<TabTitle>WriteUsers</TabTitle>

```Plain
curl --request POST \
     --url 'https://rec-api-sg1.recplusapi.com/ContentSaaS/WriteUsers' \
     --header 'accept: application/json' \
     --header 'content-type: application/json'
```



</Tab>
<Tab zoneid="z0AeVRqvAJ" title="WriteContents">
<TabTitle>WriteContents</TabTitle>

```Plain
curl --request POST \
     --url 'https://rec-api-sg1.recplusapi.com/ContentSaaS/WriteContents' \
     --header 'accept: application/json' \
     --header 'content-type: application/json'
```



</Tab>
<Tab zoneid="FFUb0ycrrM" title="WriteUserEvents">
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

<span id="a31a20a5"></span>
# Importing data to the console using API

Once you have prepared the files according to our requirements, you can proceed to import the trial data into the BytePlus Recommend console.

**To import data to the console using APIs:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

2. Click on the project you want to import data to.

   The Configure screen appears.

3. Click **Next**.

   The Import screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3eed5760e2441a583d3321fd48ff656~tplv-goo7wpa0wc-image.image) </span>

   The default import method is GCS.

4. Click the drop\-down menu and select **API/SDK**.

5. Click **Prepare resource**.

   The BytePlus Recommend team will prepare our systems to receive your imported data.

6. Import using the APIs provided.

7. Once the importing has begun, click **Import data**.

   The data import process begins in the BytePlus Recommend console.
