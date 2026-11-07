---
title: "BytePlus SMS Service Public Knowledge Base"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/FAQ"
---

<span id="ed467cd6"></span>
## API Issues

<span id="188a1281"></span>
### Q1: BytePlus returns ZJ10202 error (Invalid json param.) or sending fails due to special escape characters in content

**Answer**：This is usually caused by BytePlus failing to deserialize the SMS content, often involving special escape characters like "\n" line breaks. It is recommended to proactively encapsulate the content using map packaging before submission. (Applicable for API submission)

Example code (Java):

```Java
SmsSendRequest req = new SmsSendRequest();
req.setPhoneNumbers("xxxxxxxx");
req.setSmsAccount("xxxxxxxx");
req.setTemplateId("xxxxxxxx");
Map<String, String> param = new HashMap<>();
param.put("content", "Actual content");
req.setTemplateParamByMap(param);
```


<span id="5501d8f6"></span>
### Q2: What is the difference between APIs and OpenAPI?

**Answer**：**Authentication Complexity**


* APIs: Require integration with SDK for more complex authentication processes, providing higher security levels.

* OpenAPI: Authentication process is relatively simple, suitable for quick integration and testing.


**Template Usage**


* APIs: Must pass template ID as parameter, ensuring message content consistency and compliance.

* OpenAPI: No need to pass template ID, allowing more flexible message content.


**Reasons for Differences**


* Security considerations: The complex authentication mechanism of APIs provides higher security, suitable for handling sensitive information or large\-scale sending.

* Compliance management: Since APIs use template IDs, all sent messages can be guaranteed to have undergone pre\-review and comply with relevant regulations.

* Functionality vs flexibility: APIs provide more control and more features, while OpenAPI provides more flexibility and ease of use.


<span id="4936641e"></span>
### Q3: Why doesn't the SMS sending interface directly return SMS sending results?

**Answer**：The SMS sending interface only returns the submission status of SMS. Since SMS sending needs to be submitted to operators and then delivered by operators, it is an asynchronous process. Sending results are not returned immediately. It is recommended to configure a callback address to receive SMS sending results.

<span id="cce4a569"></span>
### Q4: The API request return value doesn't include phone numbers. How can I know the correspondence between messageId and phone numbers in this request?

**Answer**：Message IDs are returned in the same order as the submitted phone numbers.

<span id="68c327c6"></span>
### Q5: What is the difference between SMPP and HTTP access?

**Answer**：SMPP requires you to have an existing SMPP system, then submit SMS content to BytePlus through the SMPP standard protocol; HTTP refers to access through API interfaces or SDK, requiring assistance from your development team.

SMS SMPP (Short Message Peer to Peer) and HTTPS (Hypertext Transfer Protocol Secure) are two different protocols with the following main differences:


* SMS SMPP: Suitable for scenarios with high SMS sending volume requirements and need for more customized services, such as SMS gateways, SMS platforms, etc. The SMPP protocol is more complex and requires professional technical knowledge for configuration and development. For example, it needs to handle automatic concatenation of long messages, receipt of status reports, etc.

* HTTPS: Suitable for scenarios requiring protection of user data security, such as web applications, mobile applications, login pages, payment pages, etc. Developers need to integrate TLS/SSL certificates in their applications to achieve encrypted data transmission.


<span id="676e9f2c"></span>
## Frequency Control & Thresholds

<span id="bf8cf9ca"></span>
### Q1: When do console sending thresholds take effect? When are threshold intervals reset?

**Answer**：Thresholds take effect immediately after configuration. Interval resets occur at 00:00 every day (UTC+8).

<span id="091447ce"></span>
### Q2: What is the priority order of threshold configuration limits?

**Answer**：If thresholds are configured at both message group level and account level, and country\-level limits are configured under them, threshold triggering will prioritize the configuration at the lowest dimension.

Examples:


1. If the main account has a daily sending limit of 200, and a sub\-account has a daily limit of 500, and if the user sends 200 messages within a day, the main account level limit will be triggered, resulting in global messages being unsendable and returning threshold interception failure.

2. If a sub\-account has a daily sending limit of 200, and the main account has a daily limit of 500, and if the user sends 200 SMS messages under that sub\-account within a day, the sub\-account level threshold limit will be triggered, but other sub\-accounts under the same account will not be affected.


<span id="efd9735a"></span>
### Q3: Thresholds are configured but sending continues successfully. Why?

**Answer**：Thresholds take effect from the configuration time. For example, if a daily limit of 100 is configured, and the user has already sent 100+ messages before configuration, the threshold limit will only be triggered when an additional 100 messages are sent after configuration.

<span id="3a4b37af"></span>
### Q4: I configured frequency control but it's not taking effect. Why?

**Answer**：


1. Frequency control is configured at the message group level. If configured frequency control is not taking effect, first check whether SMS messages are being sent from the same message group.

2. Frequency control calculation period is from 8:00 to 7:59:59 next day (UTC+8), not starting from the frequency control configuration time.


<span id="7c5f5326"></span>
### Q5: Monthly threshold is set, and messages sent this month have exceeded the threshold, but the alert is not triggered. Why?

**Answer**：Function counting starts from the day the threshold is configured, not from the first day of the month. Therefore, you cannot look at the entire month's count; you need to calculate from the day the threshold was configured.

<span id="1867bf57"></span>
## Data Display

<span id="b11a8a34"></span>
### Q1: How can I export sending records for a specified time period?

**Answer**：SMS Console \-\> Statistics & Analysis \-\> Sending Records \-\> Export. You can self\-service export sending records with the following specified ranges:


1. Sending Date: Specify time range, maximum single export supports data within 40 days

2. Time Zone: UTC+8 or UTC+0

3. Phone Number Format: Plaintext or masked

4. Template ID: Export specific single template

5. Sending Status:a. All datab. Successc. Failured. No receipt

6. Country Code

7. Task ID


<span id="ac0aa133"></span>
### Q2: Exported sending records don't match our actual sending records. Why?

**Answer**：


1. Time zone statistics of exported sending records are inconsistent with customer sending platform statistics

2. Customer platform statistics include both SMS and WhatsApp sending data, BytePlus needs to distinguish and export these two parts separately

3. Actual sending records exceed 5 million, but sending record export has a single maximum limit of 5 million records


<span id="332ecbfe"></span>
### Q3: Export of sending records shows success but cannot be downloaded. Why?

**Answer**：You need to download the initiated export task from the export tasks section. After initiating an export task, you generally need to wait 3\-5 minutes before downloading.

<span id="39e1ff17"></span>
### Q4: What is the difference between Total submissions and Receipt success in statistics data?

**Answer**：Definitions of each field:


1. Total submissions: Total number of SMS messages submitted by customers to BytePlus

2. Total success sent: Successfully submitted to BytePlus, no submission failure data (successfully delivered to downstream)

3. No receipt received in 72h: Data with no receipt received within 72 hours

4. Failures: Receipt failure/sending failure data

5. Receipt success: Receipt success/actual sending success data


Total submissions and Receipt success represent message submission success to BytePlus and actual receipt success respectively. That is, Total submissions includes: No receipt received in 72h + Failures + Receipt success.

<span id="ab5c1478"></span>
### Q5: Why is there inconsistency between sending volume in Cost Center and SMS Console display?

**Answer**：Cost Center measures based on receipt time, while sending statistics measure based on sending time.

<span id="2b923c16"></span>
## Sending Issues

<span id="dc2d5607"></span>
### Q1: Frequency control reports CR:0202 error, but why does the interface return success?

**Answer**：SMS error codes are divided into "API error codes" and "sending status error codes".


* "API error codes": Errors during the request reception stage, which directly return error parameters.

* "Sending status error codes": Errors during the delivery stage after successful request reception, requiring configuration of callback address to receive "sending status error codes".


Frequency control checks are performed during the delivery stage, not during the request reception stage. SMS error code CR:0202 is also classified as a "sending status error code".

<span id="d1fb66d0"></span>
### Q2: SMS fails but no receipt time is returned. Why?

**Answer**：This type of failure is BytePlus interception failure, not operator return failure. You need to combine with the interception failure return error code to determine the cause of failure. Common interception code explanations:


* RE:0212: Sender does not comply with specifications. Requires input of 3\-11 English characters. Avoid passing TikTok and BytePlus related Senders.

* CR:0214: High\-risk number, usually invalid number.

* CR:0202: Frequency control interception.


<span id="c986b32f"></span>
### Q3: When sending SMS to China, phone numbers are identified as other country numbers. Why?

**Answer**：When sending SMS, phone numbers need to comply with E.164 international standards. They must start with "+", followed by country code + area code + local number. For example:


* China number: +86138XXXXXXX (+86 is country code, 138 is mobile number segment)

* UK number: +447XXXXXXXXX (+44 is country code, 7 is mobile number prefix)


This ensures cross\-border gateways correctly identify target countries, avoiding number parsing errors that result in misdelivery to other countries.

<span id="86bac4d4"></span>
### Q4: How is RE:0214 high\-risk number determined?

**Answer**：Whether a number is high\-risk is determined through user status information stored in the HLR database, such as judging whether the user is in an available state, has been suspended, is temporarily unreachable, etc. Some non\-existent numbers may be judged as unavailable and may be identified as high\-risk numbers, intercepted by BytePlus. However, since it cannot be guaranteed that a certain number is absolutely invalid, BytePlus mostly returns high\-risk number for this situation. You can treat RE:0214 error code as invalid number for judgment.

<span id="5cc78ae3"></span>
### Q5: Sending same content SMS to same phone number within short time returns same msgid. Why?

**Answer**：Volcano Engine SMS service has a default 6\-second request idempotency policy enabled. Within 6 seconds, for the same user's same phone number, submitting SMS requests with the same content will only be sent once by the system. Duplicate requests return the same msg_id, and billing only charges once.

This 6\-second time range is uniformly set and currently does not support caller self\-configuration.

<span id="0db41fc4"></span>
### Q6: Do long SMS receipts come as one or multiple messages?

**Answer**：Long SMS only receives one receipt.

<span id="bb3ce2cf"></span>
## Platform Operations

<span id="2c0fc269"></span>
### Q1: For bulk SMS function when uploading phone number lists, in what situations can I manually input phone numbers?

**Answer**：You can manually input phone numbers only when using templates that do not contain variables. If the template contains variables, you must download the template, fill in the phone numbers and variable values in the template, and then upload via the template.

<span id="b51ae6ee"></span>
### Q2: When registering BytePlus account, email verification prompts exceeding email limit

**Answer**：One email can only be bound to one BytePlus account. Different accounts need to use different emails for registration.

<span id="d297e6bb"></span>
### Q3: When binding credit card, prompt: "Adding payment method failed. The number of UIDs/Clients/merchants bound by Pl exceeds the limit"

**Answer**：One credit card can only be bound to one BytePlus account. Different accounts need to bind different credit cards.

<span id="b317422c"></span>
### Q4: Error when activating SMS service: "ErrorMessage: Usor is not authorized to perform:bill_volcanoengine:CommonBuy on resource"

**Answer**：When using IAM sub\-user to activate services, you need to grant the BillingCenterFullAccess policy to this IAM sub\-user.
