---
title: "How to Integrate ChatBI with Lark"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/How_to_Integrate_ChatBI_with_Lark"
---

<span id="8c64a6e5"></span>
# 1. Overview

DataWind supports combining large model capabilities on Lark to implement ChatBI. Before performing the configuration described in this document, you need to complete the basic configuration for integrating the Lark application.

<span id="2a893415"></span>
# 2. Configuration process

<span id="61ca03f9"></span>
## 2.1 Bind Lark to the office platform

<span id="d423408d"></span>
## 2.2 Configure the bot in the Lark developer platform

<span id="a5b12d9a"></span>
### 2.2.1 Bot request address configuration

Address format: Replace `{火山主账号ID}` with your own console account ID

```SQL
https://console.volcengine.com/bi/datawind/aeolus/api/v3/dispatcher/{火山主账号ID}/action
```


<span id="aaa39e65"></span>
#### (1) Event subscription address

<span id="435accd4"></span>
#### (2) Add event

Add an event for **receiving messages**

<span id="878aa1b0"></span>
#### (3) Message card request URL

<span id="1c2f3217"></span>
### 2.2.2 Bot permission configuration

In the permission management of the Lark application bot, locate the following 8 permissions, select them, and enable them in bulk.


|**Permission name** |**Permission ID** |
|---|---|
|Obtain basic information of the address book |contact:contact.base:readonly |
|Obtain basic information of the user |contact:user.base:readonly |
|Obtain the user ID |contact:user.employee_id:readonly |
|Obtain user ID by phone number or email |contact:user.id:readonly |
|Obtain and send one\-on\-one and group messages |im:message |
|Obtain one\-on\-one messages sent by users to the bot |im:message.p2p_msg |
|Obtain messages where users @ the bot in groups |im:message.group_at_msg |
|Receive group chat @ bot message events |im:message.group_at_msg:readonly |
