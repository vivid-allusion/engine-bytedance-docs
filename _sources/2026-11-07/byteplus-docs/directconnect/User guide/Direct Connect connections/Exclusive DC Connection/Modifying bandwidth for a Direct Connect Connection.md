---
title: "Modifying bandwidth for a Direct Connect Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Modify-dedicated-line-bandwidth"
---

After creating a Direct Connect (DC) Connection, you can still modify the maximum bandwidth of the DC Connection based on your actual needs.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The DC Connection to be modified shall be **Available** and not expired. Unavailable or expired DC Connections do not support modifying bandwidth.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select the target project and region.

3. In the DC Connection list, click **Modify bandwidth** in the **Actions** column of the target DC Connection.

4. In the pop\-up dialog box, type the bandwidth of the DC Connection you purchased from the line operator.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Dedicated Line</strong>: The modified bandwidth must not be less than <strong>the maximum bandwidth of the Virtual Interface associated with the current DC Connection</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Shared Line</strong>: The modified bandwidth must not be less than <strong>the maximum bandwidth of the Virtual Interface associated with the current DC Connection</strong>, and must not exceed <strong>the total bandwidth of all Shared Lines under the current DC Connection</strong>.   </div>
   

5. Click **Save** to complete the action.
