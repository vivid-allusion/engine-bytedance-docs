---
title: "Session Management"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Session_Management"
---

<span id="注意："></span>
# Precautions

Only applications that access the Web/JS SDK support session management, such as the web side. For specific logic, please refer to the function introduction below. While the App and Mini Program default from app launch (app_launch) to app exit (app_terminate) as a session, the time interval between the two events is as the session duration.

<span id="功能介绍"></span>
# Function introduction

<span id="会话的定义"></span>
## Definition of conversation

A conversation is a series of behaviors that users engage in while continuously active on a website. By default, if the interval between two page browsing events or two page interaction events exceeds 30 minutes, the latter will be included in the new session. On the contrary, if you close the browser or stop the operation, but continue to access within 30 minutes, you will still be included in the same session.

<span id="会话切割规则"></span>
## Session cutting rules


1. From the starting point of the user's behavior, when the duration of the visit page/behavior event is ≤ the session interval (default is 30 minutes), the current session is considered uninterrupted, and a new session is opened if an event occurs after the set session time.

2. A new session is also started immediately when visiting the website from the out\-of\-app.

3. The system time starts at 0:00 midnight, and a new session will also be generated. If the previous session does not end, it will be split in two.


<span id="会话管理"></span>
# Set session interval

After logging in and entering the DataFinder console, click **Data Management** \> **Metadata Management** \> **Session Management** in the top navigation bar to enter the Session Management page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27c84d24277746c3adb9880eb0cad3d2~tplv-goo7wpa0wc-image.image) </span>

In the session management module, you can:


* Check the session interval.

* Modify the session interval.


Under normal circumstances, we do not recommend that you modify the default duration. It should be noted that the session\-related metrics will only change after modifying the configuration here.
