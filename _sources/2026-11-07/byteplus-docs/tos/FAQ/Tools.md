---
title: "Tools"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Tools"
---

This article introduces common issues encountered when using open\-source tools to request TOS.

<span id=".5L2_55SoLWJvdG8z44CBczNjbWTjgIFzMy1zZGst562J5bel5YW36K-35rGCLXRvcy3miqXplJktaW52YWxpZHBhdGhhY2Nlc3Mt5piv5LuA5LmI5Y6f5Zug77yf"></span>
## When requesting TOS using tools like boto3, s3cmd, or S3 SDK, the error InvalidPathAccess may occur.

The TOS service does not allow Path access mode and only supports VirtualHost access mode (also called virtual host access mode). You need to modify the tool's configuration to specify VirtualHost access mode. The differences between Path and VirtualHost are as follows:


* Path access mode: the bucket name is located in the path of the HTTP URL.

* VirtualHost access mode: the bucket name is located in the domain name of the HTTP URL.


```Plain
# Path access method
https://tos-ap-southeast-1.bytepluses.com/{bucketname}

# VirtualHost access
https://{bucketname}.tos-ap-southeast-1.bytepluses.com/{bucketname}

```


<span id="64c5af56"></span>
## When installing tosutil or TOS Browser on macOS, a prompt appears saying the developer cannot be verified.

You can resolve the installation error on macOS by following these steps.


1. On the macOS desktop, click **System Settings**.

2. In the left navigation bar, click **Privacy and Security**.

3. In the **Security** section, select **APP Store and identified developers.** 

4. At **Blocked "TOS Browser" because it's from an unidentified developer**, click **Open Anyway**.

5. In the pop\-up dialog, click **Open**.
