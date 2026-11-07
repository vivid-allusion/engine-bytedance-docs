---
title: "Arrears"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Arrears"
---

When BytePlus identifies that your account is in arrears, you will receive SMS or email reminders about insufficient balance. At this point, all Pay\-as\-you\-go resources under your account will be affected. This topic only describes the status of Pay\-as\-you\-go resources under the Direct Connect (DC) service when an account is in arrears. [View Available Balance](https://docs.byteplus.com/en/docs/6269/100429#%E6%9D%BF%E5%9D%97%E8%AF%B4%E6%98%8E)

<span id=".5qyg6LS55qCH5YeG"></span>
## Rules

You can view arrears details based on bill management. When your account is in arrears, all your Pay\-as\-you\-go resources will be affected, while all your Subscription resources are unaffected. To avoid any disruption to your business, recharge promptly. For procedure, see Recharge.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can set your message subscription and notification preferences. If BytePlus identifies that your account is in arrears, it will push reminders based on your settings. For details, see Message Subscription and Notification Methods.</div>


<span id=".5qyg6LS55LuL57uN"></span>
## Overview

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Regardless of whether your instances are suspended or released, you shall settle the issued bills based on actual usage.</div>



|Billing item |Metering method |Account status |Resource status |Description |
|---|---|---|---|---|
|Outbound traffic fee |Pay\-as\-you\-go |From Day 0 to Day 14 post\-arrears |Available |When the account balance becomes negative, the account enters an arrears status. Created DC Gateways remain active and available, but new gateways cannot be created.<br><br>BytePlus continues to meter the outbound traffic egressing through DC Gateways under the account and to deduct fees from the balance.<br><br>During this period, BytePlus will use any recharged amounts to automatically settle all outstanding bills that accumulated during the arrears period. Once the arrears are cleared and the account returns to a positive balance, you will be able to create new gateways. |
|||From Day 15 to Day 22 post\-arrears |Suspended |Created DC Gateways are in an **Inactive** status. Related configurations are retained but services are suspended. They do not support attaching Direct Connect Virtual Interfaces, adding BGP Peers, or static routes.<br><br>Created DC Gateways support modifying the name and description, deleting associated DC Virtual Interfaces, detaching Cloud Enterprise Networks (CENs), and deleting DC Gateway.<br><br>During this period, BytePlus automatically deducts outstanding bills issued during the arrears period from recharges to the account. Once the arrears are cleared and the account balance is non\-negative, the status of the DC Gateway changes from **Inactive** to **NORMAL**. This restores service and allows the creation of new DC Gateways. |
|||After Day 22 post\-arrears |Released |Before releasing resources, BytePlus will send a resource reclamation notice.<br><br>DC Gateways are forcibly released. After release, the configuration and data of the DC Gateway is deleted accordingly and unrecoverable. |
