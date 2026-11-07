---
title: "Create Memory Collection"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Create_Memory_Collection"
---

This section explains how to create a new Memory Collection.

<span id="Steps"></span>
# Procedure

Click the **Create memory collection** button in the upper\-left corner of the Memory Collection list to go to the creation page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bff46c7f29e24329bbe53fb8ecbb89e8~tplv-goo7wpa0wc-image.image) </span>

On the **Create Memory Collection** page, configure the **Name**, **Description**, **Version**, and **Memory extraction configuration**. For first\-time users, we recommend selecting a built\-in template for a quick start.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df9339502b6945eb93652ae22b5a5701~tplv-goo7wpa0wc-image.image) </span>

**Core Configuration:** 

**Version:** 

**Standard Version:**  Suitable for small\-scale scenarios, supporting up to 20 million vectors and 30 QPS. This edition uses a resource\-sharing model, making it more cost\-effective.

**Ultimate Version:**  Designed for large\-scale scenarios with no limits on vector count or QPS. It supports powerful compute resources for superior performance.

**Memory Extraction Configuration:**  This configuration includes rules for event and profile memories.


|Memory Extraction Setting |Description |Illustration |
|---|---|---|
|**Event Memory** |* **Event Rule Name:**  A unique identifier for the event rule.<br><br>* **Event Extraction Method:**  Describes how to extract information and what to extract. For example, from a given conversation, extract specific events, actions, and situations. When extracting event memories, focus on key elements like explicitly mentioned events, actions taken, people involved, and time.<br><br>* **Event Field Definition:**  Defines the fields for the extracted event, including their type and content. For example:<br><br>* `summary`: Type `String`, described as "Contains the context of the event, people involved, etc."<br><br>* `event_time`: Type `String`, described as "The time the event occurred." |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/067a6e040df84809b5f4593cd3ee12f9~tplv-goo7wpa0wc-image.image) </span> |
|**Profile Memory** |* **Profile Rule Name:**  A unique identifier for the profile rule.<br><br>* **Profile Extraction Method:**  Describes the composition of the profile. For example:<br><br>* **Basic Information:**  Birthday, gender, age, name, nickname.<br><br>* **Location:**  Hometown, place of residence, frequently visited cities.<br><br>* **Interests & Preferences:** <br><br><br>\*\* **Art:**  Common art forms like painting, photography, sculpture.<br><br>\*\* **Leisure:**  Recreational activities like outings, watching movies, hot springs, karaoke.<br><br>\*\* **Games:**  Various game types like video games, board games, card games.<br><br>\*\* **Music:**  A rich variety of music genres like classical, pop, rock.<br><br><br>* **Isolated by assistant:**  Once enabled, profile updates are segregated by assistant. This means a single user will have multiple, isolated profiles (one for each assistant) that are updated independently.<br><br>* **Profile Field Definition:**  Defines the fields for the extracted profile, including their type and content. For example:<br><br>* `basic_info`: Type `String`, described as "User's basic information."<br><br>* `interests`: Type `String`, described as "User's interests and preferences." |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be62ae7101054828b4b9acf2a64211f8~tplv-goo7wpa0wc-image.image) </span> |


After filling in the information, click **Create memory collection** in the bottom\-right corner.
