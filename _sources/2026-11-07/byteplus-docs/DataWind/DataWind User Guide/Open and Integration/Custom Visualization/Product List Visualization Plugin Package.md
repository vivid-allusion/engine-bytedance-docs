---
title: "Product List Visualization Plugin Package"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Product_List_Visualization_Plugin_Package"
---

<span id="cf3f2d58"></span>
# 1. Overview

In the plugin marketplace, users can add the **product list plugin**. This plugin presents product images and key information, such as name, sales volume, price, and key attributes, in a clear and concise list format, displaying them in the form of product cards. This meets the personalized display requirements for different products. It also allows configuration to enable click\-through to web pages or dashboards, enabling users to access the most essential content in the shortest time and greatly improving information browsing efficiency. \* *(This plugin is a paid plugin package. To purchase, please contact sales.)* 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/152296bd3d8b45b6b582c8f2c4342d5f~tplv-goo7wpa0wc-image.image" width="2559px" /></div>


<span id="6122a7bd"></span>
# 2. Quick start

<span id="2c4830eb"></span>
## 2.1 Dataset requirements

The product list plugin supports displaying product images. Therefore, the dataset should include an image address field to store the **URL** of the image.

If the current base data table does not include a product image address field, a separate image table can be created. **Each product should correspond to one image address; there must not be multiple image addresses for the same product.** 

Example of an image data source:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/260e4b796e9c4c9e9cd72d2bf550d171~tplv-goo7wpa0wc-image.image" width="1525px" /></div>


Incorrect example:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da6f688c8904489aab301d4a7e674372~tplv-goo7wpa0wc-image.image" width="1796px" /></div>


After setting up the image data source, you can link the image table with the product order table or basic information table in visual modeling.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b97015e0acd400fa7e93cbbbe2b817b~tplv-goo7wpa0wc-image.image" width="2554px" /></div>


Example structure of a product basic information table:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72159e348663415b90a33f4d616bf3ee~tplv-goo7wpa0wc-image.image" width="1729px" /></div>


<span id="c3be4318"></span>
## 2.2 Usage example

**Step 1**: Go to visual query, scroll to the bottom of the "Charts" section, select the plus sign "Get from marketplace", find the product list plugin, and click Add. After adding, the product list plugin icon will appear in the chart list.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a0dab2888ea4449957666da210bd071~tplv-goo7wpa0wc-image.image" width="2559px" /></div>


**Step 2**: According to chart requirements, add product ID, product image, labels, metrics, and filters.


* Product ID: One dimension can be placed here. If "Category" is placed in the product ID, one product card will correspond to information for one category of products. If "Order ID" is placed in the product ID, one product card will correspond to the product information of one order. Generally, to make the information clearer and more concise, it is recommended to use the product name or category.

* Product image: Place the image URL here

* Label: One attribute can be added. The label will be displayed at the top right corner of the product card as a prompt.

* Metrics: One or more metrics can be added and will be displayed below the product card. The aggregation method can be configured.

* Filter: Filter options can be added; this is optional.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8276716cd9b4389871dd67d8893c6d2~tplv-goo7wpa0wc-image.image" width="2551px" /></div>


<span id="93ef9d65"></span>
## 2.3 Application scenarios

The **Product List** visualization plugin package can be widely used in the **consumer goods industry** and the **e\-commerce industry**. Specific application scenarios are as follows:


* **Market research and analysis**: Users can intuitively view the sales performance and key attributes of different product categories, quickly compare the market performance of various products, and help enterprises develop more precise market strategies. For example, when studying the beverage market, it is possible to clearly compare the sales volume, price, and key attributes that consumers care about for different beverage brands.

* **Store product management**: Quickly understand each store's product inventory, sales data, and category information through the product list, enabling reasonable allocation of goods and optimization of product displays. For example, for chain supermarkets, it is easy to grasp the sales speed and remaining inventory of fresh products in each store, allowing for timely restocking and adjustment of display locations.

* **E\-commerce store operation optimization**: E\-commerce companies can quickly view the sales performance and key information of various products in the store, enabling targeted product recommendations and promotional activity planning. For example, during major e\-commerce promotions, use the sales and price data in the product list to focus on promoting best\-selling products and discounting slow\-moving products.

* **Competitive product analysis**: Directly compare the differences between the store's products and competitors, including image display effects, price advantages, sales data, and more, to optimize product strategies. For example, in the apparel e\-commerce sector, it is possible to compare key data such as the price and sales volume of the same style of clothing across different stores in detail, identifying competitive advantages and shortcomings.


<span id="5b317156"></span>
# 3. Feature introduction

<span id="343516aa"></span>
## 3.1 Style configuration

<span id="2ca0b3dc"></span>
### 3.1.1 Label color

In the "Label color" section on the left side of the editing panel, you can set label colors, with up to five label colors available.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e12566a9694467cb8e6f2fb6e58d460~tplv-goo7wpa0wc-image.image" width="2046px" /></div>


<span id="27e48c3e"></span>
### 3.1.2 Layout and size

In the "Layout and size" section on the left side of the editing panel, you can configure the product card width, the number of cards per row, the spacing between product cards, the image aspect ratio, and the number of metric cards per row.


* You can set the product card width rule by choosing either "Fit to container" (fill the screen) or "Custom". If "Custom" is selected, you can set the product card width below.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3deab03e8e56492d8432fb0abafd8acf~tplv-goo7wpa0wc-image.image" width="2060px" /></div>



* You can set the maximum number of product cards and metric cards displayed per row. After setting, product cards and metric cards will be arranged in rows and columns according to the specified numbers.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea9c17d653bb42d5b88de0e00bc7f57f~tplv-goo7wpa0wc-image.image" width="2056px" /></div>



* You can set the spacing between metric cards.

* You can set the image aspect ratio to Default, 1:1, 4:3, or 16:9. After setting a uniform image aspect ratio, the product card layout will appear more organized.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63630d423d2d455894b02a4e21668d00~tplv-goo7wpa0wc-image.image" width="2046px" /></div>


<span id="cc6d6865"></span>
### 3.1.3 Metric name configuration

The metric names in metric cards can be modified in the "Metric" dropdown menu under "Set field information".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4df61963d1f540d59789f76becea3256~tplv-goo7wpa0wc-image.image" width="2052px" /></div>


<span id="e2a3521b"></span>
### 3.1.4 Metric unit configuration

By default, data in metric cards has no unit. In the "Metric" dropdown menu, select "Set data format" – "Number" to set a unit suffix and decimal places, making the data clearer and reducing confusion caused by missing units.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8eadf88a48f463a810bb15964f9de9c~tplv-goo7wpa0wc-image.image" width="2048px" /></div>


<span id="965a096f"></span>
## 3.2 Analysis configuration

The product list visualization plugin supports configuration for sorting, top N, percentage, comparison, and period\-over\-period analysis.


* Supports sorting product cards.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/714c685c71a34447bad02cb0489e2cf5~tplv-goo7wpa0wc-image.image" width="2559px" /></div>



* Supports displaying only the top N products.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e49057e11ece4f9684c302b1ff962048~tplv-goo7wpa0wc-image.image" width="2557px" /></div>



* Supports percentage, comparison, and period\-over\-period calculations. The results will appear in the metric cards after calculation.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe6bf00a01684cbeb0dbc57054afb7d2~tplv-goo7wpa0wc-image.image" width="2558px" /></div>


<span id="6d00fa9c"></span>
## 3.3 Navigation settings

After saving the visualization query to the dashboard, you can configure navigation in the **dashboard** so that clicking a product card navigates to a web page or dashboard. (For details, see: [Chart navigation](https://www.volcengine.com/docs/4726/67241))

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e86af261d41b401aa403f2944f6ead36~tplv-goo7wpa0wc-image.image" width="2060px" /></div>


<span id="0ccfc946"></span>
### 3.3.1 Navigate to web page

Go to the dashboard editing page, select the product list chart, click the three dots in the upper right corner, and select "Navigation settings".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c3ffad9f53a437c93d14604e1e259eb~tplv-goo7wpa0wc-image.image" width="2559px" /></div>


In the redirect settings, select 'Redirect to web page', choose the open location, and enter the target web page address in the target web page URL field. The field value `{字段名}` can be used as a parameter in the URL redirect rule. As shown in the figure, selecting the high heels indicator card will redirect to `https://www.baidu.com/s?wd=高跟鞋`, that is, it will search for "高跟鞋" on Baidu.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b238c410cca492e94c27a5b2fba622b~tplv-goo7wpa0wc-image.image" width="2559px" /></div>


<span id="467ecaa9"></span>
### 3.3.2 Redirect to dashboard

Go to the dashboard editing page, select the product list chart, click the three dots in the upper right corner, and select redirect settings.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32df1396b41b4ef1978e65524fabae7f~tplv-goo7wpa0wc-image.image" width="2559px" /></div>


Select 'Redirect to dashboard', choose the open location, and select the target dashboard from the list (only dashboards with access permissions can be selected).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83898b110df44a18920eda7d09835d9e~tplv-goo7wpa0wc-image.image" width="2559px" /></div>


To display only the data of the selected product on the redirected dashboard when clicking different product cards, the following conditions must be met:

(1) The current chart contains a filter option

(2) The target dashboard contains a public filter

(3) The filter option of the current chart has the same dimension as the public filter

After meeting these conditions, open Redirect settings \- redirect with filter conditions, and associate the current chart filter with the public filter of the target dashboard to enable dashboard redirect. As shown in the figure below, if you click the high heels product card to redirect, the public filter of the target dashboard will filter for "Product Category = High Heels", and the redirected dashboard will display only order data for the high heels category.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a0d01047be74085b448b596cd75b9a8~tplv-goo7wpa0wc-image.image" width="2552px" /></div>
