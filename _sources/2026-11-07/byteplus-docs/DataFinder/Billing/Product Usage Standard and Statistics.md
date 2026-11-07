---
title: "Product Usage Standard and Statistics"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Product_Usage_Standard_and_Statistics"
---

<span id="410ace2a"></span>
# Basic concept


* **Usage statistics criteria** : refers to different dosage calculation methods. When signing the contract, you need to choose the corresponding usage statistics criteria. There are two ways to measure the usage of BytePlus Growth Analysis, namely: **effective event volume** and **MTU** (monthly tracked user).

* **Contract period** : refers to the time period for signing a contract with the customer, such as the contract period 2020/02/02~ 2021/02/01, which is a one\-year contract period. If the contract period has not ended and the contract renewal is successful, a new contract period will be added.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The SaaS version of Growth Analytics <strong>uses event data valid for one year</strong> . That is, if an event data is reported on January 1, 2023, the event data can be used up to December 31, 2023.   </div>
   

* **Account period** : In the contract period, one natural month counts as one account period. For example, the contract period is 2019/08/15 (2020/08/14, that is, the first account period is 2019/08/15) 2019/08/31, the second account period is 2019/09/01 (2019/09/30, and the last account period is 2020/08/01) 2020/08/14.


<span id="e9317437"></span>
# Product usage criteria description


|Usage criteria description |Valid event |MTU |
|---|---|---|
|Calculation method |The sum of all valid events reported is counted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Currently, not all events are counted in event usage. For the range of valid events, see the Valid Event criteria below.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If a valid event is disabled in event management, the corresponding event is not reported and is not counted in event usage.</div><br> |According to the SSID criteria, users who have had valid events in the past month are counted.<br><br>Valid events include the following three categories:<br><br><br>* Preset events, please refer to: [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table).<br><br>* User\-defined code event tracking events.<br><br>* Events automatically reported after the SDK function is enabled include:<br><br>   * Full event tracking<br><br>   * The web page automatically collects the page dwell time<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the above event is disabled in event management, the corresponding event will not be reported and will not be counted in event usage.</div><br> |
|Calculation timing |The statistics of the previous day will be completed at 10:00 the next day. |The statistics for the previous month will be completed at 10:00 on the 1st of each month. |


<span id="e5479919"></span>
## Effective event criteria

Valid events include the following three categories:


* Preset events, the full list of preset events currently supported by DataFinder can be referred to for details: see [Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table), which excludes the following non\-valid events that will not be billed, other preset events will be billed statistically.

   ```Java
   Invalid event list:
   '_be_active',
   'bav_scheme',
   'bav2b_monitor',
   'bav2b_sdk_init_cost',
   'bav2b_sdk_start_cost',
   'bav2b_sdk_register_cost',
   'bav2b_sdk_active_cost',
   'bav2b_sdk_logsetting_cost',
   'bav2b_sdk_abtest_cost',
   'tt_fetch_did_error',
   'stream_req_stat_channel',
   'stream_req_stat_feed',
   'bav_replay'
   //'any_event' and 'any_active_event' are not real events that will be reported, but "pseudo events" after removing the event filter when using all reported events, which is convenient for you to use when querying and analyzing, so these two events will not be billed.
   'any_event'  
   'any_active_event'
   ```
   

* User\-defined code event tracking events.

* Events automatically reported after the SDK function is enabled include:

   * Full event tracking

   * The web page automatically collects the page dwell time


<span id="c3683263"></span>
# Data storage valid period description

After the data is reported to the DataFinder, the DataFinder will save it for you for a certain period of time. After the storage valid period, the historical data will be lost. The storage valid periods for each environment are as follows:


|**Environment type** |**Data storage valid period** |
|---|---|
|SaaS\-cloud native |Data is stored for a maximum of 1 year by default |
|SaaS \- Cloud Native (Cloud Hosting) |By default, data does not have a set expiration time |


<span id="c0eced57"></span>
# Check product usage

Usage statistics are located on the Group Information page managed by the Group. For groups that have signed up, whether it is a trial license or a officially signed license, you can see the event consumption of each application in the current and past license cycles on the group information page.

<span id="c1d2e3a4"></span>
## Precautions


* Account permission requirements:

   Only the **group administrator** can enter the relevant page to view the product usage details. If your current account does not find the corresponding page entrance, it may be that the authority is insufficient.

* Inquiry entrance:

   * SaaS\-Cloud Native: **Group Settings** \> **Group Project Overview**

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da2d68dabc994be48e6d45cbe751230d~tplv-goo7wpa0wc-image.image) </span>


<span id="faq"></span>
## FAQ: **How to disable events?** 

For custom events, it is disabled in "General Event Management" in "Data Management".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/589c1ada369b4f3ea1b5c04aae3d4e50~tplv-goo7wpa0wc-image.image) </span>

Circle events do not support disabling or deleting for the time being.
