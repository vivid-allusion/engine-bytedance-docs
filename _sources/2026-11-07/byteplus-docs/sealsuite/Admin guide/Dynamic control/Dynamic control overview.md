---
title: "Dynamic control overview"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-overview-of-dynamic-control"
---

SealSuite has built a comprehensive and flexible office security policy framework based on industry practice and research. With SealSuite's dynamic control function, you can customize dynamic security capabilities in alignment with the security requirements and management needs of your enterprise, thereby reducing the difficulty and cost of implementing enterprise security systems.

<span id="417abb63"></span>
# Function introduction

SealSuite's dynamic control module is associated with other modules such as identity management, device management, device baseline, DLP, and anti\-virus control. When you have configured dynamic control rules based on your security or management needs, SealSuite will continuously monitor and evaluate user behaviors and device risks. When behavior or risks that comply with specific dynamic control rules are detected, SealSuite will respond in real\-time and take actions according to the specified disposal rules within a dynamic control rule. In addition, in the dynamic control module, SealSuite will monitor and display the security status of all devices within the corporate intranet. You can use this statistical information to handle risk devices promptly. The following is a description of all the functions included in dynamic control:


|**Function** **Items** |**Description** |**Related Documents** |
|---|---|---|
|Control Policies |This is where you build the rule groups that form your dynamic security engine. When a specific trigger event occurs—such as the detection of malware on an endpoint—SealSuite will automatically execute the corresponding response action you've configured. This allows you to instantly block high\-risk threats while handling lower\-risk events with more flexible responses.<br><br>**Example:**  You can create a policy that automatically revokes an endpoint's VPN and Wi\-Fi access the moment a virus is detected. |[Configuring dynamic policies](https://docs.byteplus.com/docs/sealsuite/docs-dynamic-policies) |
|Remediation Logs |The Remediation Logs provide a complete audit trail of all automated actions taken by your Dynamic Control policies. Here, you can review which endpoints were affected and what specific response was executed. |[Viewing remediation logs](https://docs.byteplus.com/docs/sealsuite/docs-processing-records) |
|Trigger Logs |A trigger log is generated every time a user action or device state matches the conditions of a Dynamic Control policy. This log provides detailed context about the event, including the time, the rule that was triggered, the user and device involved, and the status of both the trigger and the response. |[Managing trigger logs](https://docs.byteplus.com/docs/sealsuite/docs-trigger-event-logs) |
