---
title: "HTTPS configuration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-https"
---

You can bind an SSL/TLS certificate to your domain name and enable HTTPS to increase its security during live streaming.

<span id="d1bc3916"></span>
# Applicable to


* Stream\-pulling domain names

* Stream\-pushing domain names


<span id="47193979"></span>
# Introduction to this function

**HTTPS**

HTTPS (HyperText Transfer Protocol Secure) is a transmission protocol for secure communication over computer networks. It adds SSL/TLS protocols on top of HTTP, ensuring the security and integrity of data during transmission through techniques such as digital certificates and encryption algorithms.


* **Ensuring data security**: By binding an SSL/TLS certificate to a domain and enabling HTTPS, data transmitted during live streaming is encrypted, preventing it from being stolen or tampered with, thus protecting users' privacy and security.

* **Boosting user trust**: Using HTTPS can increase users' trust in your streaming platform, enhancing user satisfaction and loyalty.

* **Complying with legal and regulatory requirements**: In some cases, using HTTPS is a legal requirement, such as in the financial and e\-commerce sectors.


**HTTP/2**

HTTP/2, the most recent iteration of the HTTP hypertext transfer protocol, was officially launched in May 2015. This updated version builds upon the capabilities of HTTP/1.x, offering enhancements like a binary framing layer, header compression, multiplexing, server push, and other functionalities. While HTTP/2 does not enforce the use of HTTPS on websites, major browsers' compatibility with HTTP/2 is contingent upon SSL/TLS implementation. Presently, websites employing HTTP/2 are expected to have HTTPS enabled.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">HTTP/2 is only applicable to stream\-pulling domain names.</div>


**TLS Versions**

Different versions of the TLS protocol vary in compatibility and security. Older versions offer better compatibility but lower security, while the latest versions provide enhanced security but may have compatibility issues. Most modern browsers now support TLS 1.3.

When you access a domain with HTTPS acceleration enabled via a browser, the caching node will select the highest TLS version that matches both the browser's TLS version and the accelerated domain's configuration. If the caching node cannot find a compatible TLS version, the TLS handshake will fail, preventing the connection from being established.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Setting TLS versions is only applicable to stream\-pulling domain names.</div>


<span id="8658adf5"></span>
# Prerequisites


* A domain name has been added

* An SSL/TLS certificate. For more information, see [Managing SSL/TLS certificates](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates).


<span id="5f81b8bf"></span>
# Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Settings** \> **Domains** to enter the domain list page.

3. On the **Domains** page that appears, find the domain name that you are about to configure and click **Settings** in the **Actions** column.

4. On the page that opens, click the **HTTPS** tab.

5. Click **Edit** to the right of the **HTTPS** toggle.

6. In the **Edit HTTPS information** dialog box that appears, **HTTPS** is turned on automatically. You must select the SSL/TLS certificate you want to use. Then, you can:

   * Enable **HTTP/2** for the current domain name.

   * Set the **TLS version range**.

7. Click **Confirm**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Your SSL/TLS certificate will appear in the <strong>Certificates</strong> list only if your domain name is added to the <strong>Subject Alternative Name</strong> field in the certificate.</div>


* <div data-tips="true" data-tips-type="tip">The HTTPS encryption takes about 10 minutes to take effect. If the configuration does not take effect, contact technical support for help.</div>
