---
title: "Authorizing a cross-account CEN"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Cross-account-authorization"
---

When you want to load a Direct Connect (DC) Gateway under your account to a Cloud Enterprise Network (CEN) under another account for private network communication, you need to add a CEN authorization within your account. Once authorized, your DC Gateway can be loaded to the CEN.

Similarly, if you want to load a DC Gateway under another account to your CEN, another account needs to add a CEN authorization. Once authorized, its DC Gateway can be loaded to your CEN.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Whether loading to a CEN under the same account or to a CEN under another account via cross\-account authorization, you can load a single DC Gateway to only one CEN.</div>


<span id=".5re75Yqg6Leo6LSm5Y-35o6I5p2D"></span>
## Add cross\-account authorization

This example demonstrates the cross\-account authorization process by loading a DC Gateway under this account to a CEN under another account If the DC Gateway and the CEN are under the same account, you can directly load this DC Gateway to the CEN without authorizing the CEN.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* Before authorizing a CEN under another account, you need to obtain the following information:

   * The CEN instance ID.

   * The main account ID of the account to which the CEN belongs.

* You can only authorize one cross\-account CEN instance for a DC Gateway.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target region.

3. Click the name of the target DC Gateway.

4. Select the **CEN cross\-account authorization** tab, click **CEN cross\-account authorization**, and type the target CEN Instance ID and its account ID.

5. Click **Authorize** to complete the action.

   After authorization, when loading an instance to the CEN within other accounts, you can select the authorized DC Gateway under your account. For instructions on how to attach network instances to CEN, see Installing a network instance.


<span id=".6Kej6Zmk6Leo6LSm5Y-35o6I5p2D"></span>
## Cancel a cross\-account authorization

If you want to limit the permissions of the DC Gateway under your account and prevent other accounts' CEN from loading your DC Gateway for interconnection, you can cancel cross\-account authorization. After canceling authorization, other accounts will be unable to load your DC Gateway to their unauthorized CENs.

<span id=".5pON5L2c6ZmQ5Yi2"></span>
### Limits


* If the DC Gateway under your account is authorized but not loaded to a CEN of another account, you can directly cancel the authorization.

* If the DC Gateway under your account is authorized and loaded to a CEN of another account, you must unload the DC Gateway from the CEN before canceling authorization.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target region.

3. Click the name of the target DC Gateway.

4. Select the **CEN cross\-account authorization** tab to view the account and CEN information authorized for the current DC Gateway.

5. Click **Deauthorize** in the **Actions** column of the target account.

6. Click **Deauthorize** to complete the operation.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [GrantInstanceToCen](https://docs.byteplus.com/en/docs/cen/GrantInstanceToCen): Authorize a specified network instance to a cross\-account CEN instance.

* [RevokeInstanceFromCen](https://docs.byteplus.com/en/docs/cen/RevokeInstanceFromCen): Cancel a cross\-account authorization of a specified network instance from a CEN instance.

* [DescribeInstanceGrantedRules](https://docs.byteplus.com/en/docs/cen/DescribeInstanceGrantedRules): Query the authorization status of a specified instance.

* [DescribeGrantRulesToCen](https://docs.byteplus.com/en/docs/cen/DescribeGrantRulesToCen): Query the cross\-account authorization of a specified CEN instance.
