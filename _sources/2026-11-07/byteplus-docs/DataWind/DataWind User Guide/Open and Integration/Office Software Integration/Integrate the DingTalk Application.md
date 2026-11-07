---
title: "Integrate the DingTalk Application"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Integrate_the_DingTalk_Application"
---

This article describes how to integrate DataWind with the DingTalk application.

<span id="ed5d9ad2"></span>
# Feature overview

DingTalk integration can be completed by creating a custom application on the DingTalk side.

**Common application scenarios**:


* Dashboard subscription

* Chart monitoring and alerting

* Push notification for dataset synchronization results


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The relevant operations must be completed by creating a custom application through the DingTalk Open Platform. The configuration interface of the DingTalk Open Platform is updated periodically. Please note that you should refer to the latest configuration interface.</div>


<span id="ed8dd0de"></span>
# Pre\-configuration instructions


1. Create an application in the [DingTalk tenant](https://oa.dingtalk.com/index.htm#/microApp/microAppList).

   1. After opening the link, click "Custom Application."

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3eecfae038528017126fbb544e0bcc19.png) </span>

   2. The web interface will redirect as shown below; click "Create."

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_60169ac782494ed2615d7cba65b19b20.png) </span>

   3. The web interface will redirect as shown below; click "Create Application."

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a212f9152fcf6addab2f4fe7c55772fe.png) </span>

2. Fill in the application information.

   You can use your preferred application name and icon to create the application.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d99abb20c310bcaf15d39184bcecd47.png) </span>

3. Configure the allowlist.

   To call DingTalk's APIs, you need to perform the corresponding security settings.

   After creating the application, the web interface will redirect as shown below; click "Security Settings."

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a6046b1637e69db9b135f4153df9d325.png) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In this step, the following configurations differ between SaaS and private deployment. Please pay attention.   </div>
   

   * For **SaaS version users**, you need to set the following IPs as the allowlist, that is, "Server Egress IP":

      180.184.64.81,180.184.87.232,180.184.102.141,14.103.128.84

      At the same time, you need to set the redirect URLs as follows:

      https://console.volcengine.com/bi/datawind/#,https://console.volcengine.com/bi/datawind#/,https://console.volcengine.com/bi/datawind#/dataManage,https://console.volcengine.com/bi/datawind/#/dataManage,https://console.volcengine.com/bi/datawind/auth#/dataManage,https://console.volcengine.com/bi/datawind/auth/#/dataManage,https://console.volcengine.com/bi/datawind#/dataPrep,https://console.volcengine.com/bi/datawind/#/dataPrep,https://console.volcengine.com/bi/datawind/auth#/dataPrep,https://console.volcengine.com/bi/datawind/auth/#/dataPrep,https://console.volcengine.com/bi/datawind/#/prep/dataLink/authCallback/lark_sheet,https://console.volcengine.com/bi/datawind/#/prep/dataLink/authCallback/lark_bitable

   * For **private deployment users**, please configure the IPs and URLs according to your company's internal settings.

4. Set permissions.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d3dc4c88435fbdae705b3b83b8bba896.png) </span>

   In the permission management section on the left, users can set application permissions and visibility scope. The following permissions are required:

   * Read permission for address book department information

   * Read permission for member information

   * Permission to obtain basic member information by phone number

   * Read permission for address book department members

   * Read permission for external contacts of the enterprise

   * Read permission for DingTalk group basic information

5. Publish the application.

   Click "Version Management and Release," then click "Create New Version" in the upper right corner.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bcf7e45a949d4752fee0b42a6d98144b.png) </span>

   After filling in the version information, click "Release" to bring the current application online.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_19b38223951db923990c3276dee509f1.png) </span>

6. Office platform integration and user account binding.

   In "Credentials and Basic Information," locate the application credentials to obtain AgentId, Client ID (that is, AppKey), and Client Secret (that is, AppSecret).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b225d181ddf52c5ac2b3ec8bd4a48703.png) </span>

   Click "Home" in the upper left corner to return.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0acf02a33b4fec52a06cba28283153a1.png) </span>

   Find the CorpId on the right side of the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d443f089a1118976bed2c524994bd29.png) </span>

   Then complete the office platform integration in Intelligent Data Insight. For details, see [Office platform integration](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628f7);

   Proceed to the user binding help documentation to bind users for both Intelligent Data Insights and DingTalk. For details, see [Overview of system administration – SaaS edition](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f62695);

   After binding, users can receive DingTalk message notifications.


<span id="a66991a6"></span>
# Integrate with the mobile platform

After completing all operations in the "**Pre\-configuration instructions**", continue with the following steps on the DingTalk application management page:

<span id="4315734b"></span>
## Configure the domain name

In Add Application Capabilities, click Add Web Application.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f6419371c4bf40226523a052c4b1a4f4.png) </span>

Then configure the application address and other relevant information in the web application.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a4cdca418594907ab5d981862b05430e.png) </span>


* Homepage: https://【域名】/bi\-h5/?corpId=$CORPID$&【地域】

* Example: If 【域名】 is [console.volcengine.com](https://docs.byteplus.com/en/docs/191/console.volcengine.com), CORPID is 12345, and 【地域】 is Shanghai, then the homepage URL is: [https://console.volcengine.com/bi-h5/?corpId=12345&region=cn-shanghai](https://console.volcengine.com/bi-h5/?corpId=12345&region=cn-shanghai);

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The access region information for the SaaS version is as follows. For more information, see <a href="https://docs.byteplus.com/docs/undefined/6a05e62618a680056d54216b">Access regions and Volcano Engine intranet connection</a>:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">North China 2 \- Beijing: region=cn\-beijing   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">East China 2 \- Shanghai: region=cn\-shanghai   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Southeast Asia \- Johor: region=ap\-southeast\-1   </div>
   

* After making changes, remember to publish the application again.


<span id="91623d78"></span>
## Mobile workspace

Pin this application to the homepage of the mobile workspace for convenient access on mobile devices.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f180881f15ba366162ae35175ea6f59f.png) </span>

<span id="24bb680b"></span>
# Message push

<span id="7fc532dc"></span>
## Push scenarios

Supports subscribing to dashboard screenshots sent to the DingTalk application. Chart monitoring messages and application dataset synchronization results will be pushed to the DingTalk application.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b0f116d75d7938ac878ebab64370321.png) </span>
