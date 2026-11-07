---
title: "How does the username conflict policy work when Configuring user-based access?"
product: "BytePlus Cloud Identity"
product_code: "CloudIdentity"
source: "https://docs.byteplus.com/en/docs/CloudIdentity/How-does-the-user-name-conflict-policy-work"
---

<span id="Nd6syTJf"></span>
### Overview

Username refers to the **user name of the Cloud Identity Center user ** , and also refers to the **user name of the IAM user under the Byteplus account ** .

> When you authorize user SSO, Cloud Identity Center will establish a binding relationship between IAM sub\-users and Cloud Identity Center users under the corresponding account. If there is already an IAM sub\-user with the same username as the Cloud Identity Center user under the current account, you can specify the action performed by Cloud Identity Center at this time through the "Username Conflict Policy".


Username conflict policy

There are three types of username conflict policies: **replace ** , **keep both ** , and **bind conflicting users ** .


|username conflict policy |Whether to create a new IAM user |Whether to delete the original conflicting IAM user |Whether to establish SSO login method corresponding to IAM users ||Whether the corresponding IAM user is deleted or retained according to the deletion policy ||
|---|---|---|---|---|---|---|
||||original conflicting IAM user |New IAM user |original conflicting IAM user |New IAM user |
|replace |Create a new IAM user with the same name |Yes |\- |Yes |\- |Yes |
|Keep both |Yes |No |No |Yes |No |Yes |
|Bind conflicting users |No |No |Yes |\- |Yes |\- |


<span id="pAeHV0ZS"></span>
#### Replace

If you select Replace, after recognizing that there is an IAM user with the same name under the target account, Cloud Identity Center will delete the original IAM user and replace it with a new IAM sub\-user with the same name. Please note that the **original user\-related authorization and data will be deleted ** . Please confirm that you no longer need the original IAM user when selecting this policy. 

The newly created IAM user with the same name under the account will be retained or deleted according to the deletion policy. Namely, with the cloud identity center user for enterprise user on\- and off\-transfer synchronization.

<span id="W1HVXTG8"></span>
#### Keep both

Select Replace, then when it is recognized that there is an IAM user with the same name under the target account, Cloud Identity Center will keep the original IAM user and will create a new IAM user with the user name added with the suffix you specified. 

Please note that the relevant authorization and data of the original user will not be affected, and only newly created IAM users with the same name under the account will be retained or deleted according to the deletion policy. That is, **the newly created user ** is synchronized with the cloud identity center user for enterprise user on\- and off\-transfer.

<span id="P49nv77b"></span>
#### Bind conflicting users

Select Bind conflicting user, then when the IAM user with the same name is identified under the target account, the Cloud Identity Center will **bind the IAM user to the current authorized task ** . If a Cloud Identity Center user is deleted, the IAM user will be retained or deleted according to the deletion policy. That is, when your enterprise identity source supports inbound and outbound transponder synchronization, the IAM user will be synchronized.
