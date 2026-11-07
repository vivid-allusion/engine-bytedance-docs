---
title: "User Details"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/User-Details"
---

DataTester's **user scrutiny** provides you with queries for individual user details and behavioral streams.

<span id="4f0fb84c"></span>
# Background information

<span id="98fc020b"></span>
## Basic concept


|Term |Detailed description |
|---|---|
|UUID、SSID |UUIDs and SSIDs are both unique identifiers for users. The main difference is that UUIDs are assigned and managed by you and your team, while SSIDs are assigned and managed by DataRanges.<br><br><br>* **UUID:**  that is,a User Unique Id, generally corresponds to the user's login id (such as mobile phone number, email) one\-to\-one. UUID is maintained by you and the team;<br><br>* **SSID:**  that is, Standardized Service ID (Standardized Service Id), is the user identity provided by BytePlus growth analysis products to mark and identify users. SSIDs are generated and maintained by BytePlus Growth Analytics and can be used by you and your team as needed.<br><br><br>See more about uuid and ssid [Supported User Unique Identifiers](https://docs.byteplus.com/docs/DataTester/Supported-User-Unique-Identifiers).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The system presets several user ID types for you: UUID, SSID, device ID (web_id, device_id, anonymous_id), and also supports you to contact the technical support staff to turn on the multi\-ID type function, manually add more ID types in the background. See the introduction and use points of multi\-ID types <a href="https://docs.byteplus.com/docs/DataTester/Advanced-Feature-Multi-Application-Multi-Agent-Multi-ID-Type">Advanced features: multi\-application/multi\-agent/multi\-ID type</a>.</div><br> |
|Behavioral flow |Behavior flow, which is a detailed behavioral trajectory of a single user presented in chronological order of events occurring on the client side. |


<span id="52578ebf"></span>
## Application scenario

Behavioral scrutiny is an extremely efficient tool for studying users and their behavior. Typical usage scenarios include (but are not limited to):


* Product & user experience team: understand the process of users using the product and make personas;

* Operations & Growth Team: Understand the user's conversion path, identify issues and improvement points that affect conversion.

* Service team: replay the user's behavior before encountering problems, and understand the product usage process of the served user.

* R & D team: Replay the user's Crash or abnormal usage behavior stream and restore the problem scene.


<span id="bc6da7ef"></span>
# Operation steps

After logging in to the DataTester product console, navigate to the left and click **Global Settings** \> **Audience Management** \> **User Detail** to enter the User Detail page, which shows the most recent 100 users who have had events that day. The page defaults to a single page to display 20.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e370b0c2099641aabccba5cc886b763a~tplv-goo7wpa0wc-image.image) </span>


* You can configure filters for user queries in Filters at the top of the page, including setting the query time range, query template, and event range for participating in the analysis (default is all).

   Among them, the scope of the query template storage includes the configuration of query conditions and query results. You can set up scenario\-based detailed examination configuration templates such as event tracking troubleshooting, feedback analysis, and abnormal reproduction. In the future, you only need to change the query ID to reuse the scene. The template will also be synchronized with other members of the project for experience precipitation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18b4feffc97047b3a5650f3f4a307a5c~tplv-goo7wpa0wc-image.image) </span>

* You can also query specific users directly by user ID, and currently support filtering to find users by UUID or SSID.

* Click a user name in the user list to jump to the user information and behavior flow details page to view the corresponding details.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If multiple applications are turned on, the user will scrutinize the behavior data of the designated user of multiple applications under the project of the default query in tandem.</div>


<span id="8226948d"></span>
## View user information and behavior streams

View user information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08614b111c2d46048e7857080703d27b~tplv-goo7wpa0wc-image.image) </span>

Include:


* User's UUID/SSID, Device ID and other ID types, first event time, recent usage, city, and other basic information.

* Information about the device that the user has recently used, such as operating system, device model, resolution, etc.

* Recent personal profile, that is, user attributes, user tags (if any), and other information related to the user. You can freely increase or decrease the display.


<span id="9d825da3"></span>
## View user behavior flow

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5de434d8c0a141c5935b4be5eef477f2~tplv-goo7wpa0wc-image.image) </span>

You can:


* Filter the behavior flow by app, device, event, property, and select important events and properties to highlight.

* View user behavior events in chronological order, and view events in reverse chronological order by default.

* Support download as csv, you can control the time period of downloading data through the time component, the maximum download time period is 30 days, the data range is the behavioral data that the page has loaded, you can drop down to load more/earlier data.

* Quick anchors are used to toggle the time of the first behavior displayed in the area of the current behavior stream, and the time range is a subset of the time range set by the overall configuration area.

* Click to view the detailed data of a single event. Currently, both list and JSON are supported. Among them, the time type attribute is converted by the current time zone by default. If you need to view the timestamp, you can switch to the json type to view the original value.
