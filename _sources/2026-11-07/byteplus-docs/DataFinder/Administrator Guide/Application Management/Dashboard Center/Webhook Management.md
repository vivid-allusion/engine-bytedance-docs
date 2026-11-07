---
title: "Webhook Management"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Webhook_Management_"
---

<span id="_1-概述"></span>
# 1. Overview

Enterprise groups such as DingTalk and Lark offer "swarm bots" in internal group chats. Add a custom bot to the enterprise group to obtain the webhook address. Using the automated enterprise group robot webhook address function, subscription and monitoring data can be pushed to the enterprise group, which is convenient for timely processing within the enterprise.

<span id="_2-设置步骤"></span>
# 2. Setup steps


* Add a swarm robot to an enterprise swarm

* Get the webhook address of the swarm robot

* Configure Webhook Address to **Growth Analysis** Webhook Management

* Create a new subscription, monitor tasks, and select the webhook address for the push channel.


<span id="_3-获取webhook"></span>
# 3. Get Webhooks

<span id="飞书-lark"></span>
### Lark /Lark


1. Open the Lark group and click Group Settings \- \> Group Robots \- \> Add Group Robots

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22fed98a09654ccf9e7d134e3dac10af~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adae7cb37da845c0babcdec3b980f426~tplv-goo7wpa0wc-image.image) </span>

2. Add "custom robot" and copy to get the webhook address.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f54155d1cc0499099fa557e67461c5d~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2722169732c436088598baf3f41fcaa~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4dd3f14c756a48c8bdc951381be1321f~tplv-goo7wpa0wc-image.image) </span>


<span id="钉钉"></span>
### DingTalk


1. Add robots to the group and add "custom robots"

2. Configure security settings and enter "custom keywords"

   Note: Added a custom keyword " **monitoring alarm"**  , the message sent by this robot must contain the word **monitoring alarm** in order to send successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_01ea15ae0a3b2ae3d08ccf88ce358216.png) </span>

    &nbsp;


<span id="wecom"></span>
### WeCom

The following is the operation process of WeCom after v4.1.41 to add push notification closure to obtain the webhook address. There may be differences in the iterative operation steps of the version. You can refer to the [WeCom official website documentation for ](https://open.work.weixin.qq.com/help2/pc/14931?person_id=1&searchData=#%E4%B8%80%E3%80%81%E3%80%8C%E6%B6%88%E6%81%AF%E6%8E%A8%E9%80%81%E3%80%8D%EF%BC%88%E5%8E%9F%E7%BE%A4%E6%9C%BA%E5%99%A8%E4%BA%BA%EF%BC%89%E4%BD%9C%E7%94%A8)operation according to the version you are currently using.


1. Open the WeCom group and click Group Settings \- \> Push Notification \- \> Add a push notification.

   <span>![图片](https://wework.qpic.cn/wwpic3az/976750__RdX8JwYRUi8njY_1754968763/0) </span>

2. Set the name and introduction of the push in the pop\-up window, and copy the webhook address of the current push message.

   <span>![图片](https://wework.qpic.cn/wwpic3az/469208_Q1Ip8paRRYymaK2_1754968766/0) </span>

    &nbsp;


<span id="slack"></span>
### Slack


1. Go to the slack application management page (https://api.slack.com/apps)

2. [Applications that have been created can be skipped] Create an application, take the From scratch method as an example: fill in the application name and select the workspace

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_868639eaebe3b276991a5f943800a708.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ee07a8354ac22e9b278ab2bd6f72751.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f962630fbb4c79198e0ec3f578aabc14.png) </span>

3. Select Apps \- \> settings \- \> add features and functionality \- \> incomming webhooks

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b8def72bf2ed63223cdcd7d09affa78.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3333e98c269b0bec22f0b5c580bed414.png) </span>

4. Open **Activate Incoming Webhooks \- \>**  Add New Webhook to Workspace

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2a577ce6da43b9a21dfe71b1d364829b.png) </span>

5. Select the channel where the app is published \- \> Allow \- \> Copy to get the webhook address

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2224a9e36d2aaa6f15c48dd4f72e441.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4d857b5c939fcc9fcafa60155bdf1487.png) </span>

    &nbsp;


<span id="_4-configure-webhook-address"></span>
# 4. Configure Webhook Address

Location: Dashboard Center \- Webhook Management

Configuration: Click New Webhook and fill in the corresponding webhook for the enterprise group. After the configuration is complete, all users under the app can use the webhook.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0ff6f67b74e4d7e9bf82fc5b6ebeec1~tplv-goo7wpa0wc-image.image) </span>

<span id="_5-使用webhook地址"></span>
# 5. Use the webhook address


* In Dashboard subscription & chart monitoring, push method \- the configured webhook address can be selected in the enterprise group.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88c263cd27094d099fb8d16e054713e6~tplv-goo7wpa0wc-image.image) </span>
