---
title: "API Description and Public Parameters"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/API_Description_and_Public_Parameters_User_Analysis"
---

<span id="d39eb7d6"></span>
# 1. Overview

This document provides an interface for querying user information, behavioral flow, tags, and other information according to the ID of different calibers.

Note: Support after privatization version 4.4 (inclusive).

<span id="7a6aec10"></span>
# 2. API public parameters

**Context\-path**: /datafinder

**Body**:

```json
{
    "query_id": "xxxx",
    "query_type": "user_unique_id"
}
```



|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|query_type |string |Yes |user_unique_id |Query caliber types, the currently supported type enumeration values are as follows:<br><br><br>* user_unique_id<br><br>* ssid<br><br>* web_id<br><br>* device_id |
|query_id |string |Yes |123456789 |Query ID |


<span id="07ad7d23"></span>
# 3. API List


|API |Explain |
|---|---|
|[Get the User's User Information, Device Information, User Tags and User Property Value](https://docs.byteplus.com/docs/DataFinder/Get_the_Users_User_Information_Device_Information_User_Tags_and_User_Property_Value) |Get the user's user information, device information, user label and user attribute value |
|[Get the User's Behavior Stream](https://docs.byteplus.com/docs/DataFinder/Get_the_Users_Behavior_Stream) |Get the user's behavior stream |
|[Create Query ID of User List](https://docs.byteplus.com/docs/DataFinder/Create_Query_ID_of_User_List) |Query ID for creating user list |
|[Get Results Based on Query ID](https://docs.byteplus.com/docs/DataFinder/Get_Results_Based_on_Query_ID) |Get results based on query id |
|[Streaming Export Based on Query ID](https://docs.byteplus.com/docs/DataFinder/Streaming_Export_Based_on_Query_ID) |Streaming export based on query id |
