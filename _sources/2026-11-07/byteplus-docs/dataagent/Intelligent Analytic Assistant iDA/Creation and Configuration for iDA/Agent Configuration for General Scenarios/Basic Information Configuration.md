---
title: "Basic Information Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Basic_Information_Configuration_"
---

This article provides you with configuration guidance related to basic information when creating and configuring an Intelligent Analytics Agent.

<span id="860e417b"></span>
# Background Information

Intelligent Analysis Agent supports two application types **on the web** and **Lark** :


* Web page: After the agent is created and launched, open the agent page directly in the browser for use.

* Lark side: After the agent is created and launched, it is integrated into the Lark application, and the agent can be directly used in the Lark application in the future.


If the agent needs to be integrated into the Lark side for subsequent use, in the basic information configuration, in addition to completing the general configuration, the Lark side needs to be configured.

<span id="32787640"></span>
# Common configuration


1. In the agent list, click Agent Configuration under the corresponding agent to enter the agent configuration interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6525378e45f344dbbcb7a866c2228539~tplv-goo7wpa0wc-image.image) </span>

2. Click Basic Information in the left navigation bar of the agent configuration page, enter the basic information configuration page, and click the Edit button in the upper right corner. You can start configuring the basic information of the agent on this page. The description of setting configuration items is as follows:

   * Basic settings:

      
      |Parameter |Configuration instructions |
      |---|---|
      |Avatar |Support users to customize the agent avatar. You can click the avatar picture to customize and upload the agent avatar picture. It also supports clicking on the avatar to select the officially provided character image for selection, and the effect preview can be performed on the right.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e52ff376f8f4f318af7f324efa4c39e~tplv-goo7wpa0wc-image.image) </span> |
      |Name & Description & Introduction |You can customize the agent name to identify the agent, and configure the summary description information and detailed introduction for the agent, so that subsequent users of the agent can quickly understand the role of the agent. Markdown format is supported when filling in the detailed introduction.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fda443ce95db4755b06d11abc9347159~tplv-goo7wpa0wc-image.image) </span> |
      

   * Agent administrator configuration:

      * In a privatized environment, the default admin user is the administrator of the agent. You can add the user as the administrator of the current agent by entering another username in the text box.

      * The agent administrator has the editing permission of the agent, and can edit, delete, publish and other operations on the agent .

         It is recommended that you combine the business team personnel of the agent, and after the overall permission control planning, configure the user personnel of the administrator according to the permission planning. The specific permission content can be referred to [Permission Management](https://docs.byteplus.com/docs/dataagent/Permission_Management).

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59fb6509ab0741c8980f03e54575714b~tplv-goo7wpa0wc-image.image) </span>

   * PC\-side agent member

      Agent administrators can perform operations such as viewing member lists, adding/removing members, and more.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77e4beb72f364b20b39a51f466517dc5~tplv-goo7wpa0wc-image.image) </span>

3. After completing the above configuration, click the "Save" button in the upper right corner of the page to save the basic information configuration result of the agent.


<span id="92925857"></span>
# Lark side configuration


* If the agent needs to be integrated into the Lark side for subsequent use, in the basic information configuration, in addition to completing the general configuration, the Lark side needs to be configured.

* When configuring the Lark side, you need to obtain the Lark callback address of the current agent first. After completing the docking configuration on the Lark application side, you can configure the agent here.

   See the end\-to\-end configuration flow for Lark [Lark-Side Intelligent Agent Configuration and Testing](https://docs.byteplus.com/docs/dataagent/Lark-Side_Intelligent_Agent_Configuration_and_Testing).
