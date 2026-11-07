---
title: "Window funnel functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Window-funnel-functions"
---

This topic describes the syntax of window funnel functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="5ef04d41"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Syntax |Description |
|---|---|---|
|WINDOW_FUNNEL |WINDOW_FUNNEL(sliding_window,<br><br>timestamp, event_id, array[event_list01, event_list02...]) |Searches for an event chain in the sliding time window and counts the maximum number of consecutive events in the event chain.<br><br>Use this syntax if the value of the event_id parameter is specified in an event chain. |
||WINDOW_FUNNEL(sliding_window,<br><br>timestamp, array[event_id=event_list01, event_id=event_list02...]) |Searches for an event chain in the sliding time window and counts the maximum number of consecutive events in the event chain.<br><br>This syntax is more flexible. Use this syntax if you want to specify values for the event_id parameter. |


<span id="2c6781fc"></span>
## WINDOW_FUNNEL

The WINDOW_FUNNEL function searches for an event chain in the sliding time window and counts the maximum number of consecutive events in the event chain. The function starts matching from the first event in the specified event chain and matches the events in sequence, then returns the maximum number of consecutive events.

<span id="52d8e918"></span>
### **Function Syntax**


* Syntax format

   * If the value of the event_id parameter is specified in an event chain, use the following syntax:

      ```SQL
      WINDOW_FUNNEL(sliding_window, timestamp, event_id, array[event_list01, event_list02...])
      ```
      

   * To specify values for the event_id parameter, use the following syntax for flexibility:

      ```SQL
      WINDOW_FUNNEL(sliding_window, timestamp, ARRAY[event_id=event_list01, event_id=event_list02...])
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |sliding_window |A sliding time window. Unit: seconds. The value is of the Bigint type. |
   |timestamp |A timestamp. Unit: seconds. The value is of the Bigint type. We recommend that you use the built\-in **time** field of TLS. |
   |event_id |A log field. The value specifies an event, such as A, B, or C. The value is of the varchar type. |
   |event_list |A custom event chain. The event chain can contain up to 32 events. The value is of the array type. Examples:<br><br><br>* ARRAY['A', 'B', 'C']<br><br>* ARRAY[event_id='A', event_id='B', event_id='C'] |
   

* Return value description

   The return value is of the Bigint type.


<span id="47d681c7"></span>
### Example


* Example 1

   * Scenario

      The statement queries the maximum number of consecutive stages that each user enters, and groups the results by `user_key`.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2241bb07f8c41cea44fce16593fba59~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      * | SELECT user_key, WINDOW_FUNNEL(86400,__time__/1000,ARRAY [stage_key='stage1', stage_key='stage2',stage_key='stage3']) AS levels GROUP BY user_key ORDER BY user_key
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f832f2bb5be14db6888b415697eb2ec4~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

* Example 2

   * Scenario

      The statement queries the maximum number of consecutive stages that each user enters, and groups the results by `user_key`.

   * Sample log

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06f1afeca3c44f4d84e19d67e5c4f61f~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
      

   * Query and analysis statement

      ```SQL
      * | SELECT user_key, WINDOW_FUNNEL(86400,__time__/1000,stage_key, ARRAY ['stage1', 'stage2', 'stage3']) AS levels GROUP BY user_key ORDER BY user_key
      ```
      

   * Query and analysis results

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e00744dbedb74d228a8c9c2e582b57cc~tplv-goo7wpa0wc-image.image" width="1282px" />      </div>
