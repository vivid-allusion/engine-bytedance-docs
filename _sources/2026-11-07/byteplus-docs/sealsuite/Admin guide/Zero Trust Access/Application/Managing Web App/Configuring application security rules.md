---
title: "Configuring application security rules"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-application-security-rules"
---

For the application that has configured the application gateway, you can establish a security policy, which includes features such as screen watermarking, copy prohibition, right\-click prohibition, and developer tool prohibition. This policy restricts browser behavior to enhance application security and access.

<span id="becaa538"></span>
# Prerequisites

The application has been added and associated with the application gateway. For more information, refer to [Adding SSO application](https://docs.byteplus.com/docs/sealsuite/docs-add-application).

<span id="9e207ce5"></span>
# Procedure


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Zero Trust Access** \> **Application**.

3. Select the application that requires the security policy and go to its details page.

4. Navigate to the **Application Gateway** tab and scroll down to the **Security Policies** section.

5. Configure the appropriate rules to restrict browser behavior and enhance application security and access.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b7b71ff218d407088e2f0d13cfcb62a~tplv-goo7wpa0wc-image.image) </span>


<span id="58c277d9"></span>
### Watermark

This policy displays a watermark above the browser when accessing applications. Currently, only visible watermarks are supported. To enable this policy, follow these steps:


1. On the right side, toggle the switch to Enable the watermark policy.

2. Click **Configure** and set the watermark style.

   SealSuite provides recommended parameters. Click **Recommended Configuration** in the upper right corner and click **OK** to quickly finish the screen watermark setting.

   
   |Item |Description |
   |---|---|
   |**Watermark Text** |Select the user information to display in the watermark. Multiple options can be selected. |
   |**Font Size** |Set the font size of the watermark text. The supported range is 8 px to 40 px. |
   |**Rotation Angle** |Set the rotation angle of the watermark text lines. |
   |**Color** |Set the font color of the watermark text. |
   |**Transparency** |Adjust the font's transparency. A lower percentage results in a more transparent watermark. |
   |**Density** |Choose how closely the watermark lines are spaced.<br><br><br>* **Loose:**  Fewer watermark lines with wider spacing.<br><br>* **Moderate:**  A standard number of watermark lines with balanced spacing.<br><br>* **Compact:**  More watermark lines with tighter spacing.<br><br>* **Custom:**  Manually adjust the row and column spacing to define a custom density. |
   |**Preview Watermark** |Click to see a preview of the currently configured watermark. |
   |**Reset to Default** |Click to restore the system's default watermark settings. |
   

3. Click **Confirm** to apply the watermark.


<span id="3ae45185"></span>
### Disable Copy Function

After the function is activated, employees will be restricted from performing certain actions such as selecting content, copying with Ctrl + C, and using the right mouse button to copy selected content when accessing the application.

<span id="7451b187"></span>
### Disable Mouse Right Click

After the function is enabled, employees will be prohibited from using the right mouse button to perform any function items, including copy, paste, download, print, save as and more, when accessing the application.

<span id="40cabe9a"></span>
### Disable Developer Tool

After the function is enabled, employees will be prohibited from accessing the browser's developer tools, including right\-click options and the F12 button, when using the application.

<span id="135e4d17"></span>
### Automatic HTTPS redirect

For applications using the HTTPS protocol, the gateway will automatically upgrade all insecure HTTP requests to HTTPS. This ensures encrypted transmission and eliminates the risk of plaintext data exposure.

<span id="c9b4ad70"></span>
### OCSP (Online Certificate Status Protocol)

Configure whether the gateway performs real\-time SSL certificate revocation checks.


* **Enabled (Default)** : Best for gateways with **internet access**. It automatically verifies that certificates have not been revoked by the CA, enhancing security and connection reliability.

* **Disabled**: Recommended for **air\-gapped or isolated internal networks**. This prevents service startup delays or port listening failures caused by the gateway's inability to reach external CA servers.


<span id="8a239201"></span>
### Smart Site Rewriting

In scenarios where internal applications reference resources or call APIs from one another, enabling this feature allows the gateway to intelligently identify linked applications.

The gateway automatically rewrites reference URLs and Cross\-Origin Resource Sharing (CORS) headers in both requests and responses. This resolves common integration failures caused by hard\-coded internal URLs, ensuring seamless cross\-application functionality in a proxied environment.
