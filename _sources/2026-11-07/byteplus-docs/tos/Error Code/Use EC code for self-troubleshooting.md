---
title: "Use EC code for self-troubleshooting"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Use-ec-code-for-self-troubleshooting"
---

When you encounter an error accessing TOS, the response body returns an EC. This article explains how to self\-troubleshoot and resolve errors using the EC code.

<span id="281d9e87"></span>
## Steps


1. Obtain the EC information from the error response.

   ```JSON
   HTTP/1.1 400 Bad Request
   
   {
       "Error": {
           "Code": "InvalidArgument",
           "RequestId": "580c15f00eca4e70d84e3c4e036d0b64-ac12****",
           "HostId": "kElQBDtQvIsxwFYgDlZVQQszhbHt****",
           "Message": "multi destination is not support",
           "EC": "0014-00000034"
       }
   }
   ```
   

2. Click [Object Storage Documentation Center](https://docs.byteplus.com/en/docs/tos/New-feature-release-notes).

3. Enter the EC obtained in step 1 in the upper right corner; in this case, it is `0014-00000034`.

4. In the right panel, click the target document to view detailed error information.
