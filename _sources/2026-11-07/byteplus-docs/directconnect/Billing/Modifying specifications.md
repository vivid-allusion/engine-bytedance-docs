---
title: "Modifying specifications"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Modification-of-instance-specification"
---

This topic describes how a line operator modifies the port bandwidth of a Shared Line for a tenant, and how to cancel a pending bandwidth modification that awaits tenant confirmation​​.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently available only for accounts with enterprise authentication completed. For procedure, see <a href="https://docs.byteplus.com/en/docs/6261/64937">Enterprise authentication</a>.</div>


<span id=".5bim5a695Y-Y6YWN"></span>
## Modify bandwidth

If the maximum bandwidth of a Shared Line is insufficient for a tenant's current business demands, to modify the port bandwidth specification, the tenant can submit an application to its line operator.


* **Upgrade**: The tenant must pay the price difference between the original and upgraded port bandwidth specifications.

* **Downgrade**: The platform will deduct the used amount based on actual usage duration from the payment and refund the difference between the remaining cost of the original bandwidth and the cost of the downgraded bandwidth. For the used amount formula, see [Non-seven-day unconditional unsubscribe explanations](https://docs.byteplus.com/en/docs/6269/81013#.5LqM44CB6Z2e5LiD5aSp5peg55CG55Sx6YCA6K6i6K-05piO).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Modifying bandwidth will not cause disruption to existing services</strong>.</div>


* <div data-tips="true" data-tips-type="tip"><strong>If the actual traffic exceeds the downgraded bandwidth after a downgrade, packet loss may occur. Carefully assess and choose an appropriate bandwidth</strong>.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Tenants: Assess the required port bandwidth specification for the Shared Line based on current business needs and contact the line operator to apply for modification.

2. Line operators: Review the tenant’s required port bandwidth specification, ensuring that after modification, the total bandwidth of all Shared Lines under the Direct Connect (DC) Connection does not exceed the connection's total bandwidth.

3. Line operators: Modify the tenant’s Shared Line according to the tenant’s requirements.

   1. Use the account of the line operator to log in to [the Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

   2. In the DC Connection list, click the name of the target DC Connection to enter the details page.

   3. Click the **Shared Line** tab, and click **Modify Spec** in the **Actions** column of the target Shared Line in the Shared Line list.

   4. In the pop\-up dialog box, set the new bandwidth specification.

   5. Click **Migrate** to complete the action.

4. Tenants: Confirm the modification details and complete the payment.

   1. Use the tenant account to log in to [the Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

   2. In the DC Connection list, click **Modify Spec** in the **Actions** column of the target Shared Line.

   3. In the popup dialog box, confirm the Shared Line name, bandwidth, and fee are correct, and then follow the console guidance to review and accept the Legal.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Please carefully read the associated terms and conditions before selecting the checkbox. Once selected, we deem that you have read, understood, and accepted all provisions.      </div>
      

   4. Click **Confirm order** to enter the cashier desk and pay the fee difference caused by bandwidth modifications. After payment, the new bandwidth takes effect immediately. The expiration time remains unchanged.


<span id=".5pKk6ZSA5Y-Y6YWN"></span>
## Cancel a modification

After modifying the port bandwidth of the tenant's Shared Line per the tenant's request, the line operator can cancel the modification at any time. Cancellation is allowed before tenant confirmation, or after tenant confirmation but before payment completion. Once the line operator cancels a modification, the tenant can no longer modify its port bandwidth.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Use the account of the line operator to log in to [the Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the DC Connection list, click the name of the target DC Connection to enter the details page.

3. Click the **Shared Line** tab, and click **Revoke** in the **Actions** column of the target Shared Line in the Shared Line list.

4. In the pop\-up dialog box, confirm the information is correct, and then click **Revoke** to complete the action.
