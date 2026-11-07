---
title: "Data Reporting Address"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Data_Reporting_Address"
---

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type. If the reporting address is set incorrectly, you will not be able to check the reported data in the future.

<span id="c8d729d2"></span>
# Precautions

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="9ae0aa48"></span>
# Data reporting address: client side


|End type |SaaS\-cloud native environment<br><br>(Southeast Asia \- Johor) |
|---|---|
|iOS |* https://gator.uba.ap\-southeast\-1.bytepluses.com |
|Android |* https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* You need to use the overseas package: 'com.bytedance.applog: RangersAppLog\-All\-global: xxx' |
|HarmonyOS |* https://gator.uba.ap\-southeast\-1.bytepluses.com |
|Web JS |* https://gator.uba.ap\-southeast\-1.bytepluses.com |
|Session Replay |* https://gator.uba.ap\-southeast\-1.bytepluses.com |
|Mini Program |* https://gator.uba.ap\-southeast\-1.bytepluses.com<br><br>* To add a whitelist to the Mini Program: https://gator.uba.ap\-southeast\-1.bytepluses.com |
|Windows / Linux |* https://gator.uba.ap\-southeast\-1.bytepluses.com |
|MacOS |* https://gator.uba.ap\-southeast\-1.bytepluses.com |
|WeChat official account |* https://gator.uba.ap\-southeast\-1.bytepluses.com |
|Flutter |* https://gator.uba.ap\-southeast\-1.bytepluses.com |


<span id="26f3dd9f"></span>
# Data reporting address: server level


|language type |SaaS\-cloud native environment<br><br>(Southeast Asia \- Johor) |Overseas BytePlus environment |
|---|---|---|
|Java/PHP/Golang |https://gator.uba.ap\-southeast\-1.bytepluses.com |* Report address: https://mcs.tobsnssdk.com<br><br>* OpenAPI Domain Name: https://analytics.byteplusapi.com |
|HTTP |* Single data upload: https://gator.uba.ap\-southeast\-1.bytepluses.com /v2/event/json<br><br>* Bulk data upload (up to 50 per batch): https://gator.uba.ap\-southeast\-1.bytepluses.com /v2/event/list |* Single data upload: https://mcs.tobsnssdk.com/v2/event/json<br><br>* Bulk data upload (up to 50 per batch): https://mcs.tobsnssdk.com/v2/event/list |
|UserProfile API |Does not involve |https://analytics.byteplusapi.com |
|Item Reporting API |Does not involve |https://analytics.byteplusapi.com |
