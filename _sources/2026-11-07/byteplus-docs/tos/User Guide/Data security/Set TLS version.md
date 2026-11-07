---
title: "Set TLS version"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set_TLS_version"
---

TLS (Transport Layer Security) is an encryption protocol that ensures the security of internet communications. TOS supports setting the TLS version, allowing you to use a specific TLS version for secure communication. This article introduces the background information and steps for setting the TLS version.

<span id="070d72b3"></span>
## Background

When establishing a TLS connection, the TOS server and client select a mutually supported TLS version. If both support multiple versions, the TOS server prioritizes the highest version it supports. After selecting the TLS version, the TOS server and client use it for encrypted data transmission.

When the TLS version setting feature is disabled, TOS supports TLS 1.0, TLS 1.1, and TLS 1.2 by default. After enabling the TLS version setting feature, you can choose to enable TLS 1.0, TLS 1.1, TLS 1.2, and TLS 1.3 protocols. To enhance security, you can specify the minimum and maximum TLS versions in the TOS console. After setting, clients can only establish secure connections with the TOS server using TLS versions within that range.

<span id="ad0a8ac4"></span>
## TLS version description

TLS protocol has multiple versions, each with different features and security characteristics. Higher versions offer greater security but have lower compatibility with older browsers.

TOS supports TLS 1.0, TLS 1.1, TLS 1.2, and TLS 1.3. The security levels of each version and their supported mainstream browsers are explained below:


|TLS version |Security notes |Supported browsers |
|---|---|---|
|TLS 1.0 |TLS 1.0 has some security vulnerabilities that can be exploited by attackers. Due to security issues, TLS 1.0 is no longer recommended for regular secure communications. |* Microsoft Internet Explorer 6+<br><br>* Google Chrome 1+<br><br>* Mozilla Firefox 2+ |
|TLS 1.1 |Some security vulnerabilities in TLS 1.0 have been fixed, enhancing the security of encryption algorithms and message integrity protection, but there are issues like insufficient key length and weak attack resistance.<br><br>Although TLS 1.1 is more secure than TLS 1.0, it still has vulnerabilities and has been gradually replaced by TLS 1.2 and higher versions. |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 22+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 24+<br><br>* Apple Safari 7+<br><br>* Opera 12.1+ |
|TLS 1.2 |TLS 1.2 limits the use of insecure encryption algorithms, introduces stronger cipher suites such as AES\-GCM, effectively resists various attacks, and provides high security while ensuring good performance and compatibility. It suits most scenarios requiring secure network communication. |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 30+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 27+<br><br>* Apple Safari 7+<br><br>* Opera 16+ |
|TLS 1.3 |TLS 1.3 simplifies the handshake process, removes insecure encryption algorithms, introduces stronger key exchange mechanisms and encryption algorithms, enhances user privacy protection, and provides higher security and communication efficiency. It is suitable for scenarios requiring high security, such as finance and healthcare. |* Google Chrome 70+<br><br>* Microsoft Edge 79+<br><br>* Mozilla Firefox 63+<br><br>* Apple Safari 14+<br><br>* Opera 57+ |


<span id="1cf15828"></span>
## Notice


* Before disabling a TLS version, ensure no client supports only that version; otherwise, that client cannot access TOS services.

* Lowering the TLS version or disabling TLS version settings may cause security risks. Exercise caution when making changes.

* Since TLS 1.2 is the current mainstream version, excluding it may prevent most clients from accessing buckets. It is recommended to include at least the TLS 1.2 mainstream version.


<span id="5025e3d4"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the **Buckets** page, click the target bucket name.

3. In the left navigation bar, select **Security \> TLS version settings.** 

4. On the **TLS version settings** page, click **Edit** and configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |TLS version setting |Enable **TLS version settings** functionality? |
   |Minimum TLS version |Set the minimum TLS version for client connections; connection requests below this version are rejected. Optional **TLS 1.0**, **TLS 1.1**, **TLS 1.2**, and **TLS 1.3**. |
   |Maximum TLS version |Set the maximum TLS version used for client connections; connection requests above this version will be rejected. Optional **TLS 1.0**, **TLS 1.1**, **TLS 1.2**, and **TLS 1.3**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum TLS version cannot be lower than the minimum TLS version.</div><br> |
   

5. After completing the settings, click **Select**.

6. In the pop\-up dialog box, click **OK**.


<span id="0aa4378a"></span>
## Related actions

**View the current TLS version in use**

Run the following command to check the TLS version used between the client and server.

```Plain
openssl s_client -connect <Bucket name>.<TOS endpoint>:443 -servername <Bucket name>.<TOS endpoint>
```


The output returns the following content:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89188321d1794c19817e6890a0757365~tplv-goo7wpa0wc-image.image) </span>
