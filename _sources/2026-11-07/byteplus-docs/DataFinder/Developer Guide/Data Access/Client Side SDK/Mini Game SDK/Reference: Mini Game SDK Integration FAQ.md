---
title: "Reference: Mini Game SDK Integration FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_Mini_Game_SDK_Integration_FAQ"
---

<span id="da29c0eb"></span>
# SDK integration

<span id="df17a2c3"></span>
## Is the Mini Game SDK instance globally unique?

Answer: Default exported instances are globally unique. But if you subcontract or build something special, it may not be the same. It is recommended to mount the default instance of the SDK on the global object, and then call the corresponding method after obtaining the default instance through the global object during use.

<span id="530e8247"></span>
## Small game, if the customer does not buy advertisements and wants to use the url to carry the utm parameter, will the utm parameter sdk be collected in this case?

Answer: By default, the Mini Game SDK will try to get the UTM related parameters from the Mini Game startup parameters: utm_source, utm_medium, utm_campaign, utm_term, utm_content. If obtained, these parameters are placed in the event public property, and will be carried on all subsequent event reports. The ability is automatically turned on, and the business does not require any processing.

<span id="436c71d1"></span>
# More FAQ

See the FAQ for more information on data access [SDK Integration & Data Reporting](https://docs.byteplus.com/docs/DataFinder/SDK_Integration_Data_Reporting).
