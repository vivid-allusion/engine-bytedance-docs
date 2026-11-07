---
title: "Message notifications for configuration tasks"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Message_notifications_for_configuration_tasks"
---

The task may fail for some reason during the execution of the task. If the user wants to detect such state changes in time, they can use the platform's message notification function.

<span id="发送方式"></span>
# sending method

Currently only notifications to users via **email** are supported.

<span id="配置联系方式"></span>
# Configure contact information

<span id="邮箱"></span>
## email

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Since the secure phone or mailbox is sensitive information, the default sub account does not have the permission to bind the mailbox independently.</div>


<div data-tips="true" data-tips-type="tip">:::There are several ways to complete the binding of the mailbox:</div>



* <div data-tips="true" data-tips-type="tip">The administrator (main account or sub account with IAM permission) directly binds the mailbox for the ordinary user: the administrator goes to the [Identity and Access Management] \- [User] page, binds the mailbox on the user's details page, and the user completes the activation after receiving the verification email.</div>


* <div data-tips="true" data-tips-type="tip">Ordinary users bind their mailboxes independently:</div>


   * <div data-tips="true" data-tips-type="tip">Step1: The administrator turns on the switch that allows normal users to change user information in [Identity and Access Management] \- [Security Settings].</div>



<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02359566659c4b918994906b72ec2480~tplv-goo7wpa0wc-image.image" width="2560px" /></div>



* <div data-tips="true" data-tips-type="tip">Step2：</div>


   * <div data-tips="true" data-tips-type="tip">Step2.1: If the user has completed the configuration of other secondary verification methods (such as mobile phone number, MFA) before binding the mailbox, he can directly complete the binding and activation of the mailbox in [Account Management] \- [Security Settings]. Otherwise, further steps are required.</div>


   * <div data-tips="true" data-tips-type="tip">Step2.2: The administrator turns on the switch of sub account management MFA device in [Identity and Access Management] \- [Security Settings], the login protection of sub account, and the secondary verification must be done through MFA when setting all sub accounts to log in \- to ensure that each sub account has the opportunity to configure MFA.</div>


   * <div data-tips="true" data-tips-type="tip">Step 2.3: Normal users log in to the console again, and will be prompted to configure MFA.</div>


   * <div data-tips="true" data-tips-type="tip">Step2.4: After completing the configuration, ordinary users go to the [Account Management] \- [Security Settings] page to use the secondary verification of MFA to complete the binding and activation of the mailbox.</div>



<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20f5112ee4b04406818e00a0cb099f03~tplv-goo7wpa0wc-image.image" width="1585px" /></div>


<span id="消息通知的场景"></span>
# <div data-tips="true" data-tips-type="tip">message notification scenario</div>


<div data-tips="true" data-tips-type="tip">At present, as long as the user has configured the contact information, the platform will send the corresponding message to the user when the following scenarios occur.</div>


<div data-tips="true" data-tips-type="tip">
|trigger scenario |Suggested approach |
|---|---|
|The platform automatically detects that the node where the task is located is faulty. |Stop the task in time to avoid unexpected failure of the task in the subsequent operation process, and also facilitate the platform to deal with the faulty machine |
|The idle resources used by the task are recycled, causing the task to be stopped |If the task is configured with retry rules, it will automatically retry without processing |
|A <code>failed</code>or <code>completed</code>state while the task is running |Pass the monitoring and log of the task in time to check the cause of the failure, and no special treatment is required when the normal operation is completed. |
|The task enters the retention phase |Log in to the task container through WebShell or WebIDE in time to check the cause of failure |
|The priorities of tasks are adjusted by someone |It is usually the human intervention of the queue administrator without special handling |
|The task running beyond the maximum running time triggers an automatic stop |Go to the console to see if it meets expectations |
|The task was stopped manually |Go to the console to see if it meets expectations |
</div>
