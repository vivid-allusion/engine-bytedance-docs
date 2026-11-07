---
title: "Building an enterprise IT service desk"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-building-an-enterprise-it-service-desk"
---

The IT application function of SealSuite Admin Console provides user feedback, help center, and quick tools. This article introduces how enterprise administrators can use IT application functions to build cloud\-based IT service desks for enterprises.

<span id="833112f9"></span>
# Background information

To solve questions such as account, device, network, and other dimensions encountered in daily office scenarios, enterprise administrators can use the IT application functions of SealSuite to build the following troubleshooting mechanisms to help enterprise users solve IT questions.


* User Feedback: SealSuite client has a built\-in question feedback portal. When users encounter IT questions that cannot be solved, they can report the questions to the SealSuite Admin Console, and the enterprise administrator can help troubleshoot and solve the question.

* Help Center: Enterprise administrators can input common office questions into the Admin Console, and these common questions will be published on the SealSuite client. Subsequent enterprise users can view the help center through the SealSuite client to obtain solutions to common questions

* Quick Tools: The Admin Console provides tools by default to assist in solving IT questions. These tools are configured by enterprise administrators based on the actual situation of the enterprise and can be applied to SealSuite client. Subsequent users may use quick tools if necessary to resolve questions encountered.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This tutorial provides example operations for building and using an enterprise IT service desk. During the actual configuration process, you can change the relevant configurations according to the actual situation and requirements of the enterprise.</div>


<span id="9e65a004"></span>
# Step 1: Building an IT service desk in the Admin Console

All operations in this step are performed by the enterprise administrator in the Admin Console.


1. Log in to the Admin Console.

   You need to use the enterprise administrator account to log in to the Admin Console.

2. Set help center.

   For specific operations, please refer to [Instruction for use](https://docs.byteplus.com/docs/sealsuite/docs-operating-instructions-).

3. Set quick tools.

   1. In the left navigation bar, click **Settings** \> **IT Tools**.

   2. In the **Service & help** section, click the **IT Assistant** card. Complete the following configurations on the **Configure IT Assistant** page, and click **Confirm**.

      * Set **Display** **Icon**.

      * Set **Assistant name**, for example `Obtain IT service`.

      * Set **Redirect link**. You need to set redirect link according to actual needs. If your enterprise solves IT questions through Lark group chat on duty, you need to set up a link for SealSuite group chat. You can click **Guide** in the **Configure expert services** interface to view the specific settings for links.

   3. Turn on the **IT Assistant** function switch.


<span id="4aaf96e0"></span>
# Step 2: Using IT service desk on SealSuite client

This step is for enterprise administrators to test whether the IT service desk function is effective on the SealSuite client.


1. Log in to the SealSuite client.

2. In the left navigation bar, click **Help**.

3. View the configured frequently asked questions document in the **Help Center** interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5de55bf627404655aa8a12e40a26dab3~tplv-goo7wpa0wc-image.image) </span>

4. In the Help Center interface, click **IT HelpDesk**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/485f92ce93f246f287e23dbe8f18dfce~tplv-goo7wpa0wc-image.image) </span>

5. In the left navigation bar, click **Overview**. Click **Feedback** in the **Toolbox** area and submit the question.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbcc791b63b2468eb4b7864e94de9ff3~tplv-goo7wpa0wc-image.image) </span>

   After submitting question feedback to the SealSuite client, you can log in to the Admin Console and view the corresponding question feedback on the **IT application** \> **User Feedback** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/065c9b44d4f641bb996e1651caee8705~tplv-goo7wpa0wc-image.image) </span>

   In the **Action** column, click **View information** to view **User's Feedback** and network diagnostic results. You need to contact the corresponding users to investigate and resolve the issue.

6. On the left menu bar, click **Lab** and use the **Network Diagnostics** function.

   The SealSuite client will detect your current device network environment and generate alerts for abnormal issues. You can solve the questions on your own, or click **Feedback** to provide feedback and submit the question to the Admin Console.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The feedback channels for one\-click feedback and question feedback are the same, both require the enterprise administrator to log in to the Admin Console and view the corresponding question feedback on the <strong>IT application</strong> \> <strong>User Feedback</strong> page.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00c87489e26f43d09493374d0a3fa326~tplv-goo7wpa0wc-image.image) </span>

7. On the **Lab** page, click DNS **Reset**, which supports selecting automatic reset or manual DNS reset to solve network questions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8048c8a7cbfd47e4b731426530e2f694~tplv-goo7wpa0wc-image.image) </span>
