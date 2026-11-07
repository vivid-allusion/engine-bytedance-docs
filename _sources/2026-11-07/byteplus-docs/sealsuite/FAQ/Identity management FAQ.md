---
title: "Identity management FAQ"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-identity-management_1"
---

In the process of using the SealSuite identity management module, you can refer to the following frequently asked questions and solutions when you have questions.

<span id="ffa1c9d3"></span>
## Does it support turning off account password login and using only third parties to log in?

The account password login function is not supported. Currentoly, only the priority displayed by configuring the login method is supported. You can set it in the account configuration of the SealSuite Admin Portal. The higher the sorting on the left, the higher the priority. The first priority is the primary login method of SealSuite, while the others are the secondary login methods.

Currently, the account password login method is not supported, but the priority of the login method can be set. In the account configuration of the Admin Portal, **Login Method Display Order** can be set. The higher the sorting on the left, the higher the priority. The first priority is the primary login method of SealSuite, while the others are the secondary login methods.

For specific operations, please refer to [Managing account settings](https://docs.byteplus.com/docs/31/9108) and [LDAP organizational architecture import configuration tutorial](https://docs.byteplus.com/docs/31/9120).

<span id="cadf4d6f"></span>
## Does it only support dynamic passwords when a single member initiates two\-factor authentication?

Yes. Currently, two\-factor authentication defaults to dynamic passwords, and single members do not support using SMS verification codes for two\-factor authentication.

<span id="12a317aa"></span>
## Does importing an organization structure from a new data source overwrite the old data if you have already imported it?

If you have already imported the organizational structure, when you import it again from a new data source, the new data will be compared to the old data. If the third\-party platform ID, phone number, or email in the new data matches the corresponding entry in the old data, the old data will be overwritten. If the new data does not match the old data, a new data entry will be created in the organizational structure.

<span id="e4ac9fb7"></span>
## Is there a number limit for departments and sub\-departments?

There is currently no limit on the number of departments and sub\-departments.

<span id="14db9a6e"></span>
## After the official purchase of SealSuite, will the original organizational structure be retained during the trial period?

After the trial period ends, the original data will be retained for 7 days. During this period, the official purchase of SealSuite will retain the original organizational structure. After more than 7 days, all your configurations and data will be released and cannot be restored.

<span id="7e1a79e3"></span>
## How to configure DingTalk as a data source for synchronization and third\-party authorization login?

For specific operations, please refer to [Importing organizational data from DingTalk](https://docs.byteplus.com/docs/31/9118).

<span id="0f5a71ff"></span>
## How to configure Lark as a data source for synchronization and third\-party authorization login?

For specific operations, please refer to [Importing organizational data from Lark](https://docs.byteplus.com/docs/31/9117).

<span id="95bc6027"></span>
## How to delete old data after switching data sources?

Currently, deleting old data is not supported.

<span id="22c905f6"></span>
## How to fill in the request address in the event subscription of Lark Open Platform?

When the Admin Portal creates the Lark data source connection, it will automatically generate a prompt link, as shown in the following figure, which can be copied and used.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3dbcf7e8109e42e1aafa6026bb8551b1~tplv-goo7wpa0wc-image.image) </span>

<span id="d135f629"></span>
## How to obtain cases of docking with third\-party applications?

Please go to [Submit work order](https://console.volcengine.com/workorder/create?step=2&SubProductID=P00000756) to obtain.
