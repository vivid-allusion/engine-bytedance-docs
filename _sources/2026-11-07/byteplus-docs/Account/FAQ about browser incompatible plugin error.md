---
title: "FAQ about browser incompatible plugin error"
product: "BytePlus Account"
product_code: "Account"
section: "Document"
source: "https://docs.byteplus.com/en/docs/Account/FAQ_about_browser_incompatible_plugin_error"
---

<span id="_1-issue-background"></span>
### 1. Issue Background

When your browser has incompatible plugins (such as Requestly), these plugins can inject scripts into web pages and modify native methods like `fetch` and `xhr` after the page loads. This can result in failed requests when accessing the Volcano Engine website.

Due to the inability to fully defend against plugin modifications to the `fetch` and `xhr` methods within the webpage code, and the lack of a universal fix that can be applied across different plugins, switching to another plugin might result in different errors. We recommend completely disabling conflicting plugins.

**How can you determine if the issue is caused by a plugin?** 

Here’s how to troubleshoot the problem using the Requestly plugin as an example.


* **Note**: The Requestly plugin for Chrome allows modification of network requests on web pages. Incorrect configurations can lead to authorization failures in Feishu Cloud Docs, CSRF validation errors, and other issues such as blocked website interfaces or page errors when accessing Volcano Engine.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b7d78c8f0ac19c3c7382091fd88a128c.png) </span>

\-Note: The Requestly plug\-in of the chrome browser provides the function of modifying the web page network request. Incorrect configuration will cause the authorization of Feishu Cloud Document to fail and the csrf verification to fail, resulting in problems such as the website interface being blocked and the page error when you access the Volcano Engine.

<span id="_2-troubleshooting-steps"></span>
### 2. Troubleshooting Steps

1） If you encounter the following error when accessing Volcano Engine through your browser, but you can access the site without errors in an incognito window, it's likely caused by a plugin.

2） Open the browser’s Extensions page (chrome://extensions/), check if the Requestly plugin is installed. If it is, disable it, then reopen a new Volcano Engine page and test the access. If Requestly is not installed, systematically disable other plugins to identify the conflicting one.

<span id="_3-solution"></span>
### 3. Solution

<span id="solution-1-temporary-fix"></span>
#### Solution 1: Temporary Fix

You can use your browser’s incognito mode to access Volcano Engine without issues, or use a browser without any installed plugins. For Chrome, you can open an incognito window as follows:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d25386a45d75c57c02e17e81166be058.png) </span>

<span id="solution-2-long-term-fix"></span>
#### Solution 2: Long\-term Fix

To permanently resolve this issue, you will need to completely disable the plugin.


* **Important**: Make sure to disable the plugin from the Extensions page (chrome://extensions/). Simply closing the plugin window will not fully disable the plugin.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_66cba2314c923ada4f7d6ac37adfecc9.png) </span>

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d0659ecc4bc6a1e4a4d2271a9edd93b6.png) </span>
