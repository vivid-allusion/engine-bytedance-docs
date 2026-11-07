---
title: "LAS"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/LAS"
---

<span id="_1-概述"></span>
# 1. Overview

Smart Data Insight supports connecting to the Lakehouse Analysis Service (LAS) to obtain data, create datasets, and perform further analysis. Data connections support direct connection or extraction from LAS data sources.

Before connecting to LAS, collect the following information:


* The IP address and port number of the server where LAS is located.

* The username and password for LAS.


For information on how to obtain the server's IP address and port number, refer to [BI connection](https://www.volcengine.com/docs/6492/101901)

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) On the page, select LAS.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2559fdbbabe74f37ad3aa3e766d1e556~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/038bf61c5ec64087bcb09b0e2898cc6e~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

(5) You can use this connection as a data source to create a dataset: click Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as **steps (2) and (3) in 2.1**. After completing these steps, you will remain in the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A new extraction link is added to the LAS connection (requires product version V2.58.0 or above).</div>


Add a new extraction link to the LAS connection under data connections. The LAS extraction link no longer uses JDBC, but instead directly exports data to CDP HDFS. The following diagram illustrates the comparison between the old and new links:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63610dc0ff0d4435b69255b5f8e171ef~tplv-goo7wpa0wc-image.image) </span>
