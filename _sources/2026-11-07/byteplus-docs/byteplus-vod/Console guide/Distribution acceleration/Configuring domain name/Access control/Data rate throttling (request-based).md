---
title: "Data rate throttling (request-based)"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-data-rate-throttling"
---

This article describes how to configure download rate limits in the BytePlus VOD console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The download rate limits apply to <strong>Custom\-origin domain</strong> <strong>name</strong>.</div>


<span id="1ec662ee"></span>
## Introduction

To control costs and improve user experience during traffic bursts, you can configure download rate limits for your custom\-origin domain names in the BytePlus VOD console. This guide provides step\-by\-step instructions on how to set up rules based on file type, directory, or full path to manage your CDN's peak bandwidth.

<span id="b2ff19e0"></span>
## Configuring download rate limits


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Click the **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Access control** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **Data rate throttling**, switch the **Status** toggle and select the HTTP request methods that you want to disallow.

   
   |**Configuration** |**Description** |
   |---|---|
   |Priority |Indicates the priority of the rule. If there are multiple rules, the rules are executed according to the priority. You can adjust the priority of rules by dragging and dropping. |
   |Frequency |Indicates how often the speed limit occurs. You can specify any day or days between Monday and Sunday. You can also specify **Daily**. |
   |Time period |Indicates the time period when the speed limit occurs, accurate to the minute. |
   |Rule type |Select a speed limit rule type. The configuration values are as follows:<br><br><br>* **File suffix**: The speed limit rule applies to all files with a specific extension.<br><br>* **File directory**: The speed limit rule applies to all files under a specific directory.<br><br>* **File full path**: The speed limit rule applies to a specific file.<br><br>* **Any file**: The speed limit rule applies to all files. |
   |Rule |Enter the rule content according to the specified rule type. Rule content cannot exceed 1,024 characters. You can enter one or more configurations in the rule content, and multiple configurations are separated by English semicolons (;).<br><br>The requirements for the content of the rules are as follows:<br><br><br>* If **Rule type** is **File suffix**, you need to enter one or more file suffixes. Such as `xlsx` or `png;txt`. The file suffix can contain English letters and numbers.<br><br>* If **Rule type** is **File directory**, you need to enter one or more directory paths. The input requirements for the directory path are as follows:<br><br>   * Directory paths must start and end with a backslash (/). For example `/www/img/png/;/www/doc/`. If you want to specify all directories under the accelerated domain name, enter `/`.<br><br>   * Directory paths may contain printable ASCII characters, except for:<br><br>      * Sequential slash (//), percent sign (%), space, dollar sign ($), question mark (?), Delete (ASCII code 127).<br><br>* If **Rule type** is **File full path**, you need to enter one or more file paths. The input requirements for the file path are as follows:<br><br>   * The file path must start with a backslash (/). For example `/www/img/turtle.png;/doc/study.docx`.<br><br>   * The file path supports the use of wildcards (\*) to represent one or more consecutive characters.<br><br>   * The file path can contain printable ASCII characters, except for:<br><br>      * Sequential slash (//), percent sign (%), space, dollar sign ($), question mark (?), Delete (ASCII code 127).<br><br>* If **Rule type** is **Any file**, you cannot enter any rule content, because the rule will take effect on all files at this time. |
   |Threshold |Indicates the download speed threshold. If the download speed of a request exceeds this threshold, the request will be throttled. The lowest speed you can specify is 1 B/S and the highest speed is 1,000,000 GB/S. The unit conversion used for this configuration is 1,024. |
   |Effective after |Indicates the initial download data volume for which the download speed will not be limited. For a single request, after reaching this initial download volume, if the download speed reaches the download speed threshold, the request will be throttled. If 0 is specified, the CDN monitors the download speed of the request from the first byte it downloads. The maximum initial download size you can specify is 1,000,000 GB. The unit conversion used for this configuration is 1,024. |
   

8. Click **Save**.
