---
title: "Dashboard"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Dashboard__"
---

<span id="64eeafac"></span>
# Dashboard permission

<span id="3f437c9b"></span>
## How can the group administrator give the project administrator permission to edit and save all Dashboard boards?


* DataFinder has preset the project administrator role for you. By default, this preset project administrator role has the editing and management rights of all Dashboard boards in the current project.

* If you want to give a user the editing permission of all Dashboard boards under all projects, you can create a new IAM sub\-account. When controlling the policy permission of the sub\-account, a new role is created. I hope to grant this role the editing permission of all Dashboard boards (all Dashboard refers to)


<span id="aba3ba47"></span>
## The Dashboard I made has been authorized to be edited by others. Why can't the diagrams in the Dashboard be edited? Do the diagrams have to be re\-authorized?

After Dashboard authorizes others to edit, the editing rights of the charts in the Dashboard need to be authorized separately. Otherwise, the charts in the Dashboard still do not have editing rights. Only after authorization can you edit and save the charts created by others.

<span id="ae9fa783"></span>
# Dashboard Data & Monitoring

<span id="be26983d"></span>
## How to merge charts from multiple Dashboard boards?

You can choose to add existing charts to a Dashboard board, and add the charts of other Dashboard boards that need to be merged to the current Dashboard board to merge the charts of multiple Dashboard boards.

<span id="37487ce4"></span>
## How can we continuously monitor and alert important data?

In Dashboard, we can keep an eye on fluctuations in key data by creating monitoring tasks. According to the monitoring rules, it can automatically determine whether the indicator fluctuates within the normal range, and trigger an alarm (email) when abnormal, without manual daily tracking and judgment, to achieve automatic monitoring. Monitoring task settings please refer to [Monitoring Management](https://docs.byteplus.com/docs/DataFinder/Monitoring_Management) the help documentation.

<span id="e9356e4f"></span>
# Dashboard subscription

<span id="f6c82efb"></span>
## After reading the version of Finder and subscribing, what is the reason for not receiving the email after clicking Test for a few minutes?

Check whether the email is configured. If not, the customer needs to provide email information, including email address, email port, whether to use SSL or TLS protocol, etc.

<span id="5e3cd241"></span>
## After subscribing to Dashboard, some charts in the generated long screenshots are truncated, resulting in incomplete display, especially charts with scroll bars. What should I do?

This is due to the length limit of long screenshots, charts with scroll bars cannot be displayed in full when screenshots are taken, for example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6b80f1de7b94ec6a19a86b0b1cf9e83~tplv-goo7wpa0wc-image.image) </span>

In this scenario, it is recommended to split the Dashboard board into smaller sections, each containing about 10 reports, to reduce the problem of truncation when taking screenshots.

<span id="99443297"></span>
# Other abnormal operations

<span id="7b313385"></span>
## Demo environment creates Dashboard exception: An error is reported when the Demo Dashboard is saved

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a0d4bc7ead646e29472fef25d413491~tplv-goo7wpa0wc-image.image) </span>

Solution: In the experience demo environment, product restrictions are made for the stability of the environment, such as charts, Dashboard, etc. There is a limit on the number of saves. If the maximum number of creations is exceeded, an error will be reported. In case of an error, please contact BytePlus technical support personnel to deal with it.
