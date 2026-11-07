---
title: "Workflow Management"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Workflow-Management"
---

<span id="一、功能简介"></span>
# Introduction to functions

In order to pursue stable iteration, do not want some radical strategy experiments to start or roll out 100% of the impact of the product, some scenarios want to Feature release volume before the increase in the approval process, in order to reduce the impact of misuse on the line. In addition, for some more significant function iterations, we hope to have more links such as closed testing and testing for a small amount of traffic to ensure the safety of the release before the release is launched.

However, the introduction of approval and other links will increase the overall process of feature release, and the increase in the process will inevitably affect the flexibility; while some fast\-iterating businesses and emergency bugfixes hope to be launched quickly, without more process blockages.

We integrate the demands of security and flexibility in different scenarios, and we use approval, internal testing, etc. as one of the links to support different business processes (such as which links are required for feature release, whether approval is required, etc.).

**Scenario 1: Feature Release of Important Functions**

A short video APP plans to introduce live broadcast function, first open the experiment for a period of time after the results of remarkable conclusions, plans to solidify the experiment as Feature release roll out 100%. However, the live broadcast function is a large function iteration, which needs to be operated cautiously, so it is hoped that the experimental solidification of such important functions needs to be approved by the business line administrator, and then gradually gated release after approval.

**Scenario 2: Feature release of emergency bugfix**

The login function of an APP has a flash back phenomenon. After inspection, it is found that there is a small bug. After being fixed, it is verified in the testing environment. If you want to quickly release the full amount of this Feature and quickly reduce the user experience problem, you need to release it quickly. Do not want more processes such as approval.

<span id="二、如何使用"></span>
# How to use


* Function entrance: [Global Settings] \- [Workflow Management] \- [Process Settings]

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51245d0cb71b4eceb25d693cf07ae2d2~tplv-goo7wpa0wc-image.image) </span>

* In workflow management, click the corresponding process and click Edit to set which links are required for the process

   * Confirm Feature Information: System Default Steps (On by default, not closed)

   * Approval: Approval rules can be set

      * Approval level:

         * Level 1 approval (default): i.e. only Level 1 approval

      * Approver

         * Set the default approver: role (default), name/email address, you can choose more

         * The default is app administrator and group administrator, and the administrator is supported to add others as the default approver.

         * Allow to add by yourself: not checked by default. If checked, a single task can add an approver by itself when initiating approval.

      * Pass mechanism: 1 person passes immediately (default), more than half passes immediately, and all passes immediately

      * Rejection mechanism: Reinvite after rejection (default), cancel after rejection

      * Approval notification: Send notification to the corresponding personnel (Owner, approval sponsor, approver) when the approval status changes, optional Lark (mailbox, other IM tools can be considered in subsequent iterations), multiple selections

      * Open by default, administrators can close this step

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ca303d6eda94304b87d3ecee45df639~tplv-goo7wpa0wc-image.image) </span>
