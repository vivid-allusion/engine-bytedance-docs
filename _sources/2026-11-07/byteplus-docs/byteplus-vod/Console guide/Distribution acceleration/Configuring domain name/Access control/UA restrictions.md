---
title: "UA restrictions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-ua-restrictions"
---

To control which users can access your resources, you can configure User\-Agent (UA) restrictions based on the client's HTTP request header. This guide provides step\-by\-step instructions on how to set up UA allowlists and blocklists for **Playback**, **Image**, and **Custom\-origin domain names** within the BytePlus VOD console.

<span id="2d7a2d99"></span>
## Introduction

User\-Agent is a field in the HTTP request header that contains information such as the operating system version, CPU type, and browser version of the requesting client. The web server can return user\-specific pages based on the value of the User\-Agent header.

You can allow or prevent specific users from accessing your domain name through the value of the User\-Agent field.

<span id="11c59f0f"></span>
## Configuring the UA allowlist and blocklist


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter a specific space.

2. Click **Distribution acceleration \> Domain names** on the left navigation bar.

3. Depending on the type of your domain name, click the **Playback domain name**, **Image domain name**, or **Custom\-origin domain name** tab.

4. Find the domain name you want to configure and click the **Configure** button in the **Action** column.

5. Click the **Access control** tab.

6. Click the **Modify** button at the bottom of the page.

7. Under **UA allowlist and blocklist**, switch the **Status** toggle and configure the UA restrictions:

   
   |**Configuration** |**Description** |
   |---|---|
   |Type |The optional values for this configuration are as follows:<br><br><br>* **Allowlist**: Only if the User\-Agent request header of the user request is in the allowlist, the request can access your resources.<br><br>* **Blocklist**: If the User\-Agent request header requested by the user is in the blocklist, the request to access your resources will be rejected.<br><br><br>If the User\-Agent header of a request matches the blocklist or does not match the allowlist, BytePlus VOD will reject the request and return a 403 response status code. |
   |Allowing Empty User\-Agent |Specifies whether to allow requests with empty User\-Agent headers or requests without a User\-Agent header to access your resources. |
   |User Agent Strings |Enter one or more User\-Agents. The configuration cannot exceed 30,000 characters in length. You can enter up to 1,000 User\-Agents. Also, User\-Agent is case\-sensitive when matching. The User\-Agent you entered has the following requirements:<br><br><br>* You can use wildcards (\*) to represent any number of characters. But `*` can only appear at the beginning and end of a User\-Agent.<br><br>* User\-Agent cannot contain `**`.<br><br>* A User\-Agent string must contain only printable ASCII characters, except for the Delete character (ASCII code 127).<br><br>* Separate multiple User\-Agent strings with a newline.<br><br>* A User\-Agent string cannot consist only of spaces. |
   

8. After completing the configuration, click **Save**.
