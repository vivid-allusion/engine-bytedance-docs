---
title: "WeChat Official Account Related Events and Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/WeChat_Official_Account_Related_Events_and_Properties"
---

<span id="事件及属性"></span>
## Events and properties

Need to combine WeChat official account background event interface document [event push ](https://developers.weixin.qq.com/doc/service/en/guide/product/message/Receiving_standard_messages.html), [ordinary events ](https://developers.weixin.qq.com/doc/service/en/guide/product/message/Receiving_standard_messages.html). Of which:


* wechat_subscribe/wechat_unsubscribe/wechat_scan/wechat_location corresponds to the event push in the WeChat event.

* Others correspond to ordinary events.

* wechat_template_send_finish event is a special preset event, after the data is reported, you can find it on the general event page of data management.



|Event name |Event display name |Property |Property value type |Fields corresponding to the WeChat background |
|---|---|---|---|---|
|wechat_subscribe |Official account attention |subscribe_scene |string |subscribe_scene |
|||qr_scene |string |qr_scene (value when scanning code only) |
|||qr_scene_str |string |qr_scene_str (value when scanning code only) |
|wechat_unsubscribe |Official account clearance | | |Corresponding WeChat event unsubscribe |
|wechat_scan |Official account scan code |qr_scene |string |qr_scene (value when scanning code only) |
|||qr_scene_str |string |qr_scene_str (value when scanning code only) |
|wechat_location |Report geographic location |latitude |string |Latitude (corresponding to WeChat event LOCATION) |
|||longitude |string |Longitude (corresponding to WeChat event LOCATION) |
|||precision |string |Precision (corresponding to WeChat event LOCATION) |
|wechat_menu_click |WeChat menu click |key |string |EventKEY (corresponding to WeChat event CLICK/VIEW) |
|wechat_text_message |Send this message to the official account |message_type |string |MsgType |
|||message_id |numberic |MsgId |
|||content |string |Content |
|wechat_image_message |Send a picture message to the official account |message_type |string |MsgType |
|||message_id |numberic |MsgId |
|||media_id |string |MediaId |
|||pic_url |string |PicUrl |
|wechat_voice_message |Send a voice message to the official account |message_type |string |MsgType |
|||message_id |numberic |MsgId |
|||media_id |string |MediaId |
|wechat_video_message |Send a video message to the official account |message_type |string |MsgType |
|||message_id |numberic |MsgId |
|||media_id |string |MediaId |
|||thumb_media_id |string |ThumbMediaId |
|wechat_shortvideo_message |Send a short video message to the official account |message_type |string |MsgType |
|||message_id |numberic |MsgId |
|||media_id |string |MediaId |
|||thumb_media_id |string |ThumbMediaId |
|wechat_location_message |Send location message to official account |message_type |string |MsgType |
|||message_id |numberic |MsgId |
|||location_x |string |Location_X |
|||location_y |string |Location_Y |
|||scale |string |Scale |
|||label |string |Label |
|wechat_link_message |Send a link message to the official account |message_type |string |MsgType |
|||message_id |numberic |MsgId |
|||title |string |Title |
|||description |string |Description |
|||url |string |url |


<span id="用户属性"></span>
## User properties


|Property name |Property value type |Property description |Corresponding WeChat user field |Property description |
|---|---|---|---|---|
|{WeChat appID}. wechat_openid | | |openid |As web_id |
|wechat_language |string |User language (WeChat) |language | |
|{WeChat appID}. wechat_subscribe_time |string | |subscribe_time |The attention time as the user's user_register_time, involving historical data import |
|{WeChat appID}. wechat_unionid |string |UnionID |unionid | |
|{WeChat appID}. wechat_remark |string |WeChat Remarks |remark | |
|{WeChat appID}. wechat_tagid_list |list |WeChat user tag id |tagid_list |The tag that will be typed to the user in WeChat, as the list property of the user: wechat_tagid_list: Save the WeChat user tag id list wechat_tag_list: Save the WeChat user tag name, where the conversion of tagid to tag name refers to [this interface](https://developers.weixin.qq.com/doc/service/en/guide/product/unionid.html) |
|{WeChat appID}. wechat_tag_list |list |WeChat user tag |ditto |ditto |
|{WeChat appID}. wechat_groupid |string | |groupid |ditto |
|{WeChat appID}. wechat_qr_scene |string |scan code related |qr_scene | |
|{WeChat appID}. wechat_qr_scene_str |string |scan code related |qr_scene_str | |
|{WeChat appID}. wechat_subscribe_scene |string |WeChat Follow Source |subscribe_scene | |
|touch_point |string |Official account appid |Official account appid | |
|web_id |string |Openid as webid computation source (can be switched to unionid) |openid/unionid | |
