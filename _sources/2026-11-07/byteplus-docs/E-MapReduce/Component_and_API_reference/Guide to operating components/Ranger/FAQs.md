---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ranger-faqs"
---

This article summarizes the FAQs encountered when using Ranger.

<span id="_1-新导入用户，无法在-ranger-ui-中找到？"></span>
## 1 Newly imported users cannot be found in the Ranger UI?

User management on the control side creates or imports new users, writes user information into the cluster's LDAP, and then synchronizes the relevant user information to the Ranger database through Ranger Usersync. The current synchronization interval is one minute. Please wait a moment before proceeding with the relevant permission configuration.

<span id="_2-ranger-ui-上不可添加用户或对用户密码进行编辑？"></span>
## 2 Users cannot be added or user passwords edited in the Ranger UI?

Volcano Engine E\-MapReduce (EMR) provides a permission management module. To support this module, corresponding adaptations have been made to Ranger, which restrict some functions in the Ranger UI. At this stage, users can contact customer service to enable the permission management feature via [FAQs](https://docs.byteplus.com/docs/E-MapReduce/109413).
