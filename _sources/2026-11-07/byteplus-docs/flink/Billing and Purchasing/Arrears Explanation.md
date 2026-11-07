---
title: "Arrears Explanation"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Arrears_Explanation"
---

After your account is in arrears, your resources will enter a grace period during which resource usage will be limited; if the grace period is exceeded, your resources will be forcibly reclaimed and cannot be restored once reclaimed. Please avoid having your account in arrears as much as possible.

<span id="d9ba8efe"></span>
## Arrears Handling Rules

BytePlus Flink currently uses a pay\-as\-you\-go model, with billing cycles per hour. If the available credit (account balance and vouchers) in your account is less than the unsettled bill, it will be considered as arrears.

The following are the rules for handling after an account becomes overdue:


|**Duration of Arrears** |**Description** |
|---|---|
|Arrears within 24 hours |The system will continue to maintain the resource pool instance running normally, and you can continue to use the service normally. |
|Arrears exceeding 24 hours |Account is in arrears **for more than 24 hours** and the bill arrears have not yet been paid, the service of **BytePlus Flink** will be suspended.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the bill arrears are paid within 7 days after service suspension, the system will immediately resume service.</div><br> |
|Service suspension exceeds 7 days |The system will forcefully release the resource pool instance and reclaim resources.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Once the resource pool instance is reclaimed, the data cannot be restored.</div><br> |
