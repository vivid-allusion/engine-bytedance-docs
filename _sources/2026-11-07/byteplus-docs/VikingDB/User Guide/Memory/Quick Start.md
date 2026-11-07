---
title: "Quick Start"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Mem_Quick_Start"
---

<span id="3f51e474"></span>
## Activating Viking Memory

Log in to your Byteplus account and [activate Viking Memory](https://console.byteplus.com/common-buy/VikingDB_Memory%7C%7C7291580783171539244) in the console.

<span id="9006dab9"></span>
## Creating a Memory Collection

Create a new memory collection in the Viking Memory console or by calling the [CreateCollection](https://docs.byteplus.com/en/docs/VikingDB/create_memory_collection) API. When creating, you can choose:


* Use the built\-in memory extraction template (recommended for first\-time users)

* Customize memory extraction configuration (suitable for scenarios with personalized needs)


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d1f9bc738a84586bc66646d91a076ed~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07f4f453452048bf96ebe397578faa68~tplv-goo7wpa0wc-image.image) </span>

<span id="e3854178"></span>
## Writing Original Data

Call the [AddSession](https://docs.byteplus.com/en/docs/VikingDB/add_session_to_memory_collection) API to write session data to the memory collection created in the previous step. The system will process and store these messages according to the memory extraction configuration (event rules, profile rules) of the memory collection to form structured memory events and possibly update associated profiles.

**Note:** 

When calling the AddSession API, if the same session_id is used, the system will overwrite the user profiles and events generated in that session. It is recommended to dynamically generate session_id using UUID to ensure independence for each session; reuse it only when overwriting is truly necessary.

<span id="a3a2e8ff"></span>
## Viewing Memories

After writing is complete, you can view the memories extracted by the system in the console:


* User list:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b5ac0dc9f0e4cc78bffff626281974f~tplv-goo7wpa0wc-image.image) </span>


* Profile memories:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf6ad368b5024a489222f15024eebf9b~tplv-goo7wpa0wc-image.image) </span>


* Event memories:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b608cf8d9714f30a3847be2bdb4952a~tplv-goo7wpa0wc-image.image) </span>

<span id="8793d928"></span>
## Retrieving Memories

After completing data writing, you can first test memory retrieval in the console.

**Tips:** 


* To reduce unnecessary overhead, Viking Memory builds indexes by default only after writing data.

* Index construction takes approximately 3–5 minutes. Therefore, it is recommended to wait for index construction to complete before retrieving data.

* After the index is created, it takes approximately 15 seconds for a new session to become searchable.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f78393103704f928cf74d9cd7c1edf7~tplv-goo7wpa0wc-image.image) </span>

In a production environment, please call the [SearchMemory](https://docs.byteplus.com/en/docs/VikingDB/search_memory_collection) API to implement retrieval.


* Retrieving events: You need to provide the user_id or assistant_id, or both. It is recommended to perform retrieval during each conversational turn.

* Retrieving profiles: You can provide either the user_id or the assistant_id, but not both. It is usually sufficient to perform a retrieval once at the beginning of a session.
