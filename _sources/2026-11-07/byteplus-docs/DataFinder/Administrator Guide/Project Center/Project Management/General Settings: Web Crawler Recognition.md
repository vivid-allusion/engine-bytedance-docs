---
title: "General Settings: Web Crawler Recognition"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/General_Settings_Web_Crawler_Recognition"
---

Sometimes our products encounter web crawlers. During data analysis, the data brought by these crawlers has no analytical value and affects real data. The "crawler data filtering" function launched by BytePlus Growth Analysis is to help customers better deal with web crawler data, find and process data with crawler characteristics, and support the marking or filtering of this part of the data. This article introduces the relevant rules and configuration points for crawler recognition.

<span id="48185ca6"></span>
# Function introduction

DataFinder allows you to manually configure custom crawler characteristics rules in the general settings of the project. The custom crawler characteristics rules will be recognized when the data flow module processes the reported data, and you can further set whether the recognized crawler data needs to be intercepted and put into storage.

<span id="a17a2424"></span>
# Operation entrance

After logging in and entering the DataFinder console, click **Project Center** \> **Project Management** \> **General Settings** in the top navigation bar. On the General Settings page, you can configure the crawler rules. The interface is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6a9aa6281974c86a7db314c96164404~tplv-goo7wpa0wc-image.image) </span>


* You can configure custom crawler rules in the pop\-up page by clicking the link **Configure crawler rules** .

* You can also choose whether to turn on the **recognition rules for web\-side data configuration crawlers and the processing method after recognition** switch.


<span id="c9d759f9"></span>
# Configuring crawler recognition rules

<span id="2c21d976"></span>
### Configure custom crawler feature rules


1. Add custom crawler features to pop\-up pages.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/557d0eadbd0843d1b1dac057f458d5c4~tplv-goo7wpa0wc-image.image) </span>

   * Custom rules require regular expressions, based on UserAgent, with one feature per line; up to 1000 lines are supported.

   * Custom rules only affect T + 1 data.

2. Configure the crawler filtering method. You can choose to "**mark as crawler**" or "**filter and not save**".

   * Marked as a crawler: Events identified as crawlers will be stored normally, and the value of event item $is_spider will be marked as true.

   * Filter and not save: Events identified as crawlers will be intercepted and will not fall into the library.


<span id="14638ed5"></span>
# Configure the Web\-side data crawler rule effect switch

Configuration rules need to take effect on the web.


* Open: The crawler rule is applied to the web side, but not to the other side.

* Close: Crawler rules are not valid on all ends.
