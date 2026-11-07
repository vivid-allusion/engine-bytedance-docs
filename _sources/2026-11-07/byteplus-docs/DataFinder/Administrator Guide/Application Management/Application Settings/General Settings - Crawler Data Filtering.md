---
title: "General Settings - Crawler Data Filtering"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/General_Settings_-_Crawler_Data_Filtering"
---

Sometimes our products encounter web crawlers. During data analytics, the data brought by these crawlers has no analytical value and affects real data. The "crawler data filtering" function launched by BytePlus Growth Analysis is to help customers better deal with web crawler data, find and process data with crawler characteristics, and support the marking or filtering of this part of the data. This article introduces the relevant rules and configuration points for crawler recognition.

<span id="e4174646"></span>
# Function introduction

<span id="40cfde7a"></span>
## Preset crawler feature system rules


* The data flow function module of DataFinder system has preset the crawler feature recognition rules for you, which already includes common crawler scenarios. When the useAgent of the network request contains the following characteristics, the system will automatically recognize it as a crawler event.

   ```Plain
   "msnbot|Sosospider|Sosoimagespider|Sogou web spider|Googlebot|Baiduspider"  
   
   "360Spider|YoudaoBot|YandexBot|EasouSpider|Mediapartners-Google|APIs-Google|AdsBot-Google" 
   
   "JikeSpider|MJ12bot|ia_archiver|Rogerbot|exabot| DOCOMO Sprider" 
   
   "python-requests|HttpClient|Go-http-client|Python-urllib|gohttp|curl/|Surf/|Scrapy"
   ```
   

* When recognized as a crawler event, the DataFinder will mark the value of the crawler recognition attribute $is_spider of the corresponding event as true when the data falls into the database.


<span id="d27a0f5f"></span>
## Custom crawler feature rules

DataFinder also supports you to manually configure custom crawler characteristics rules in the general settings of the project. The custom crawler characteristics rules will be recognized when the data flow module processes the reported data, and you can further set whether the recognized crawler data needs to be intercepted and put into storage.

After setting a custom rule, during the data flow phase, the current project uses custom rules to identify relevant data for interception, that is, custom rules override preset system rules.

<span id="ab6c5ede"></span>
# Operation entrance

After logging in and entering the DataFinder console, click **Application Management** \> **Application Settings** \> **General Settings** in the top navigation bar. On the General Settings page, you can configure the crawler rules. The interface is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6a9aa6281974c86a7db314c96164404~tplv-goo7wpa0wc-image.image) </span>


* You can configure custom crawler rules in the pop\-up page by clicking the **Configure crawler rules** link.

* You can also choose whether to turn on the **recognition rules for web\-side data configuration crawlers and the processing method after recognition** switch.


<span id="d4fee084"></span>
# Configuring crawler recognition rules

<span id="7cae790c"></span>
### (Optional) Configure custom crawler feature rules

The DataFinder system has preset crawler characteristic rules for you. If you do not want to use the rules preset by the system and want to use custom rules for crawler identification interception, you can click the link of the page **Configure crawler rules** to define crawler characteristic rules in the pop\-up page configuration.


1. Add custom crawler features to pop\-up pages.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The custom crawler feature defaults to null, indicating that preset rules are used; if you add a custom rule, the custom rule overrides the system's preset rules.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10cd7f22f749443b812d77271b0cdc03~tplv-goo7wpa0wc-image.image) </span>

   * Custom rules require regular expressions, based on UserAgent, with one feature per line; up to 1000 lines are supported.

   * Custom rules only affect T + 1 data.

2. Configure the crawler filtering method. You can choose to "**mark as crawler**" or "**filter out of storage**".

   * Marked as a crawler: Events identified as crawlers will be stored normally, and the value of event item $is_spider will be marked as true.

   * Filtering does not enter the library: Events identified as crawlers will be intercepted and will not fall into the library.


<span id="7c4c8821"></span>
# Configure the Web\-side data crawler rule effect switch

Configuration rules need to take effect on the web.


* Open: The crawler rule is applied to the web side, but not to the other side.

* Close: Crawler rules are not valid on all ends.


If you add a custom rule, after turning on the switch, the custom rule will override the preset non\-global rule, and the crawler rule will take effect as follows.


|**Rule type** |**Switch on** |**Switch Off** |
|---|---|---|
|**Custom rules** |Take effect |Does not take effect |
|**Presets \- Rules** |Not valid, overwritten by custom rules |Does not take effect |
