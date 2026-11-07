---
title: "Report Interpretation: Heat Map Analysis Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Report-Interpretation-Heat-Map-Analysis-Experiment"
---

<span id="一-概述"></span>
# 1. Overview

Based on the user's clicking and staying behavior on the page, it is very intuitive to visualize the behavior of a large number of users through heat maps. The heat map drawn by clicking on the location can visually see the area clicked by the user, which is convenient for discovering opportunities for conversion, or abnormal behavior that occurs within the webpage or app. This paper mainly introduces the heatmap scenario related to user click behavior and the way to create heatmap.

<span id="二-使用场景"></span>
# 2. Usage scenario


* **When a comprehensive and intuitive understanding of user behavior occurs on a page is required**

   Although other analytical methods can also provide some page\-related data metrics, their correlation is low and requires mastery of some analytical methods. The page heat map makes up for this deficiency, it is more intuitive and simple, anyone can quickly grasp and understand its meaning.

* **When the user's click behavior changes before and after the page revision needs to be compared**

   You can compare the heat maps before and after the revision, and you can intuitively understand the difference in the user's click position. It is relatively simple to determine the effectiveness of the revision.

* **When it is necessary to further determine whether there is abnormal traffic in combination with clicking**

   Some current traffic boosters can not only simulate visits, but also further create clicks. In response to this situation, if we only look at the data, we can only see an increase in traffic, but the conversion is not good. We determined by ua that it was not a crawler, but were unable to further locate other characteristics of these flows. But by clicking on the heat map, we can very intuitively find that these clicks are often concentrated in one point, or a few points, or very evenly distributed in certain positions on the page. This way, it can be judged that there is abnormal traffic behavior, providing an important basis for subsequent positioning problems.

   The important point here is that the heat map should not only contain links or buttons, but also other clicks on non\-clickable elements, because clicks on some non\-clickable elements can better expose potential opportunities and problems.


<span id="三-使用范围"></span>
# 3. Scope of use

Currently supports **visualization/multi\-link experimental reports** and heat map analysis to help you intuitively and quickly compare the effects of different experimental versions.

<span id="四-快速入门"></span>
# 4. Quick Start

<span id="_2-1-实验创建"></span>
## 2.1 Creation of experiments

In the "Create Experiment" settings for visual experiments and multi\-link experiments, you can turn on the option of [Whether to turn on heat map], and turn on heat map after connecting to the SDK. For details, see [Data Access Overview](https://docs.byteplus.com/docs/DataTester/Data-Access-Overview).)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69d5630b65c74fdd8bda36da53d96cc9~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-热力图分析"></span>
## 2.2 Heat map analysis

Experimental report \- heat map analysis, currently supports [click heat map] and [element heat map], [browse depth map] and [attention distribution map] and other functions are being improved. If you have any needs in this regard, you can contact customer service for feedback.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49f085a803e946a392a5b66482c90c62~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-1-点击热力图"></span>
### 2.2.1 Click on heat map

It is suitable for observing the specific click behavior of users to gain insight into the interaction optimization of the page. (For example, find out which parts of the page attract the attention of most users through the heat map, and further optimize; find out where users often click on some non\-connections/elements through the heat map, and consider adding clickable links/elements at that location)

Page elements include:


* The core metric data of the experimental version and the control version:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7987e65d2d347aba9eb8dac744e9eef~tplv-goo7wpa0wc-image.image) </span>

   1. Clicks: The number of any clicks (whether or not clicked on an element/link) on the page or a matching page used to render the heatmap.

   2. Bounce rate: (1\- the conversion rate of entering the next page when used as a landing page) \* 100%;

   3. Average Duration of Stay: The average length of stay for users entering the page or matching the page under the filter criteria.

* Experimental and control heat maps

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8470e894bc342c1a55f3c9ff3aecbc3~tplv-goo7wpa0wc-image.image) </span>

   1. Time Filter, Filter Dimension, Heat Map Type, Refresh, and Scroll are valid for each version of the heat map at the same time.

   2. Each page supports multiple area circles (capped at 5).

   3. When the mouse is moved to the heat map, the number of clicks, number of clicks, click percentage and click through rate information are displayed for that location.

   4. You can adjust the heat map display intensity and layout at the top right of the interface. Note: Only after hiding the heat map can you click and query the page, otherwise you can only consult the current page.


<span id="_2-2-2-元素热力图"></span>
### 2.2.2 Element heat map

The use scenario of element heat map is mainly that users need to automatically generate heat map through event tracking information, paying special attention to the heat situation (click situation) of the core event tracking part, which is often used to optimize button shape, position, etc.

Page elements include:


* Click on the Top 20 for elements of the experimental and control versions:

   1. According to the control group + experimental group, the total clicks are sorted from high to low to show the top 20 elements with the most clicks. The abscissa is the name of the element for event tracking, and the ordinate is the number of clicks. You can see the number of clicks and proportion of the corresponding group when you hover the mouse on the histogram.

* The core metric data of the experimental version and the control version:

   1. Clicks: The number of any clicks (whether or not clicked on an element/link) on the page or a matching page used to render the heatmap.

   2. Bounce rate: (1\- the conversion rate of entering the next page when used as a landing page) \* 100%;

   3. Average Duration of Stay: The average length of stay for users entering the page or matching the page under the filter criteria.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/568e2fe6c59f491680a574b89d8dc326~tplv-goo7wpa0wc-image.image) </span>


* Experimental and control heat maps

   1. Time Filter, Filter Dimension, Heat Map Type, Refresh, and Scroll are valid for each version of the heat map at the same time.

   2. Each page supports multiple regional circles (currently up to 5 are supported. If you have more needs, you can contact customer service students for feedback).

   3. When the mouse moves to the heat map, you can view the number of clicks, number of clicks, click percentage and click through rate information for that location.

   4. You can adjust the heat map display intensity and layout at the top right of the interface. Note: Only after hiding the heat map can you click and query the page, otherwise you can only consult the current page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27c6ca1c510e40e7b79147e237f63ccd~tplv-goo7wpa0wc-image.image) </span>
