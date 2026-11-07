---
title: "Short Link"
product: "Byteplus GMP"
product_code: "datagmp"
source: "https://docs.byteplus.com/en/docs/datagmp/Link_Tool"
---

<span id="b79cba93"></span>
### **1. Product Overview**

SMS length is limited, so it is often necessary to insert short links to reduce the number of characters. GMP provides the "Link Tool" capability, which supports converting long URLs into short links (including user\-specific short links, mini program short links, etc.), and tracks PV and UV. Short link creation entry: Marketing Strategy \- Content Management \- Link Tool, the default domain for created short links is: zvip.cn.

<span id="a7a26b04"></span>
### **2. Usage Restrictions**


| **[📢 Prerequisite for Using This Feature]**  ||
|---|---|
|**Activate GMP permissions** |Administrator activates permissions for the Short Link Tool (optional), Permission path: Marketing Strategy \- Content Management \- Link Tool |


<span id="d9147c28"></span>
### **3. Function Description**

 **(1) Add New Short Link**

Short links come in three types: general short links, long URL with parameters to short link, and mini program short links.


| |**Description** |
|---|---|
|**General Short Link** |**A general short link is a fixed connection generated short link**<br><br>**Validity Period**: Expires upon reaching the set date, permanently valid. If set to expire, an expiration date must be provided. The validity period cannot exceed 1 year; periods beyond a year can only be set as permanent.<br><br>**Track Click UV**:<br><br>If not tracked, then all user\-generated short links are the same, making it impossible to track click UV data.<br><br>Statistics: Generate different short links for different users to track Click UV. If you need to track which users clicked the short link, you must set "Click UV: Statistics".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb29897f39934cf2aebb84fddf5d2958~tplv-goo7wpa0wc-image.image) </span> |
|**Convert long link with parameters to short link** |**Convert long link with parameters to short link, allowing insertion of ID,and attribute parameters identifiers.** <br><br>**Validity**: Expires after the specified period; Permanently valid. If expiration is chosen, input of expiration date is required, validity cannot exceed 1 year; if it exceeds one year, it can only be set to permanent.<br><br>**Original link**: Supports insertion of User Attributes and User ID<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0d3bfd9d9a6483ea77765d3d8eb79f2~tplv-goo7wpa0wc-image.image) </span> |
|**Mini Program short link** |**Clicking a Mini Program short link directly activates the Mini Program.** <br><br>**Expires after the specified period**: Fill in the expiration date, validity period up to 3 months.<br><br>**Usage Scenarios**<br><br>WeChat Mini Program links support generating up to 500,000 original long links per day for each mini program. Each link supports only one user click. To maximize the quota, two scenarios are provided:<br><br>Generated with GMP task: Used in scenarios such as message delivery tasks and process canvas through the insert short link feature, different short links are generated for different users after the click, generating an original long link and consuming quota per user—supports tracking click UV and dynamic query.<br><br>Universal Mini Program Short Link: Only one short link is generated; each click generates a new original long link and consumes one original link quota, does not support tracking UV or dynamic queries.<br><br>**Mini Program**: Select an integrated mini program.<br><br>**Mini Program page path:**  It must be an existing page of a released mini program, cannot carry a query, and will redirect to the homepage if the path is empty.<br><br>**Startup query parameters:** <br><br>Only supports numbers, uppercase and lowercase English letters, and some special characters: !#$&'()\*+,/;:=?@\-_~<br><br>Short links generated with tasks allow insertion of user attributes, labels, IDs, etc. as variables in the startup query, whereas universal short links only support fixed queries.<br><br>**Fallback link:**  Used as a fallback link displayed when retrieving WeChat Mini Program links fails.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af456861d8d04246b346ccda30aee202~tplv-goo7wpa0wc-image.image) </span> |


<span id="c7e57dba"></span>
### **4. Short Link Management List**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bed794c9681343e78fb4553c409d7d24~tplv-goo7wpa0wc-image.image" width="858px" /></div>



|**Field** |**Field meaning and use** |
|---|---|
|**Original long link** |If there are parameters in the original long link, they should be marked in orange. Display style: hover to show the full link content. The original long link of the mini program displays the mini program name and path; hover to display the mini program name + mini program page path + startup query parameters. |
|**Short Link Type** |**General short link**: Convert long links into short links<br><br>**Parameterized long to short link**: Supports sending parameterized long links to different users which are then converted into short links, like links with different order numbers for different users<br><br>**Mini program short link**: Long links are generated via the WeChat interface and then converted into short links; optional support for counting UV, acquiring tokens to call the WeChat interface requires authorization in Channel Management. Used for scenarios such as opening mini program short links outside of WeChat, in apps like SMS and browsers. |
|**Short Link Status** |Permanently valid, expired |
|**Click PV, Click UV** |Non\-personalized short link UV displays "No statistics" |
|**Actions** |**Data Trend**: Displays data corresponding to the short link click trends, supports daily and hourly queries for PV and UV, with the date selection limited to the valid period.<br><br>**Download Details**: Supports downloading detailed short link data, and the detailed report shows the clicking user ID and the corresponding clicked link.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b139d513aeec427ea2ab25e474bb8f8d~tplv-goo7wpa0wc-image.image) </span> |


&nbsp;
