---
title: "User Event Dataset"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Introduction_to_Behavior_Dataset"
---

A user event dataset is a structured collection of user interaction data, such as clicks, favorites, and purchases. By uploading this data, you enable the system to build user interest profiles, which are essential for powering personalized search rankings and high\-precision recommendation systems. This guide details the required data format and provides sample data to help you prepare and upload your behavior data correctly.

 &nbsp;

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a945dd2aa2324daaa2eeffa46263b939" width="532px" /></div>


&nbsp;

<span id="afd7a409"></span>
# User Event Dataset 

Before uploading the user event dataset, you need to prepare user behavior log data according to requirements. 

To ensure the system identifies your data accurately and efficiently, please make sure that your logs include the key fields listed below. You may use the existing field names from your current system.

Refer to the table below for behavior dataset types:


|**Dataset type** |**Data table definition** |**Supported content input** |
|---|---|---|
|User event dataset |Records of user interactions with content or products, which must include key fields (user ID, item ID, behavior type, timestamp, etc.). |* User identifier<br><br>* Item identifier<br><br>* User event type<br><br>* Event timestamp<br><br>* Event Scene<br><br>* Other information |


<span id="514ec9df"></span>
# Required Data


|**Field Name (Example)**  |**Field type** |**Required?**  |**Field Attribute** |**Field Description** |
|---|---|---|---|---|
|user_id |`*String*` |**`Required`** |User identifier |The user's unique ID<br><br>*For example, "user\-12345".*  |
|item_id |`*String*` |**`Required`** |Item identifier |The unique ID of the item that the user interacts with.<br><br>*For example, "SWEATER\-001".*  |
|event_type |`*String*` |**`Required`** |Action type |**User event types:** <br><br><br>* exposure<br><br>* click<br><br>* like<br><br>* favorite<br><br>* share<br><br>* comment<br><br>* follow<br><br>* add cart<br><br>* purchase<br><br>* Custom events |
|event_timestamp |`*Int64*` |**`Required`** |Timestamp |The time when the behavior occurred<br><br>*For example, 1729507800000.*  |
|event_scene |`*String*` |**`Required`** |Event Scene |The scene where the action occurs. <br><br>*For example, a user completes a purchase on the "Shopping Cart" page.*  |


&nbsp;

<span id="dd304e22"></span>
# **Sample Data**

The following examples illustrate a complete behavior journey for a user — from browsing an item to adding it to the cart and finally completing the purchase:

```Plain Text
// 1. Exposure: System recommends the sweater on the homepage.
{
    "user_id": "user-12345",
    "item_id": "SWEATER-001",
    "event_type": "exposure",
    "event_timestamp": 1729507200000,
    "event_scene": "home",
    "device_os": "IOS"
}

// 2. Add to Cart: User shows interest and adds it from the product detail page.
{
    "user_id": "user-12345",
    "item_id": "SWEATER-001",
    "event_type": "add cart",
    "event_timestamp": 1729507320000,
    "event_scene": "product_detail_page",
    "device_os": "IOS"
}

// 3. Purchase: User completes the conversion on the shopping cart page.
{
    "user_id": "user-12345",
    "item_id": "SWEATER-001",
    "event_type": "purchase",
    "event_timestamp": 1729507800000,
    "event_scene": "shopping_cart",
    "device_os": "IOS"
}
```


&nbsp;

&nbsp;
