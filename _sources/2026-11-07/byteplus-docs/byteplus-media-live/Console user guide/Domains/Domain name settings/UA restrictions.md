---
title: "UA restrictions"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ua-blocklist-and-allowlist"
---

The User\-Agent (UA) is an HTTP request header that contains information such as the operating system and browser version of the client making the request. You can allow or prevent specific users from accessing your domain name through the value of the UA header in the pull streaming requests.

<span id="630434dd"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. Find the domain name that you want to configure, and click **Settings** in the **Actions** column.

4. Click the **Access control** tab.

5. Click **Edit** to the right of the **UA restrictions** toggle.

6. In the **Edit UA blocklist and allowlist** dialog box that appears, configure the following parameters.

   
   |**Configuration** |**Description** |
   |---|---|
   |List type |The options for this configuration are as follows:<br><br><br>* **Blocklist**: If the UA header in the user request is included in the blocklist, the request will be rejected and a 403 status code will be returned.<br><br>* **Allowlist**: Only if the UA header in the user request is included in the allowlist will the request be able to access your resources. Any other requests will be rejected and a 403 status code will be returned. |
   |Rules |Enter one or more UA headers which cannot exceed 30,000 characters in length. You can enter up to 1,000 UA headers.<br><br><br>* UA headers are case\-sensitive.<br><br>* You can use wildcards (\*) to represent any number of characters. `*` can only appear at the beginning or end of a UA header. You can add `*` to both the beginning and end of a UA header, such as `*curl*`.<br><br>* The UA header cannot be `*`.<br><br>* The UA header cannot contain `**`.<br><br>* The UA header must contain only printable ASCII characters, except Delete (ASCII code 127).<br><br>* You should enter one UA per line.<br><br>* The UA header cannot contain spaces only. |
   |Include empty UA headers |Specifies whether the configuration applies to requests that contain an empty UA header or do not contain a UA header. For example, if you set **List type** to **Blocklist**, and set **Include empty UA headers** to **Include**, requests that contain an empty UA header or do not contain a UA header will be rejected. |
   

7. Click **Confirm**.
