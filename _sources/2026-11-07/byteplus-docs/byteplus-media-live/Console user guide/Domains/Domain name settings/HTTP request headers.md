---
title: "HTTP request headers"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-http-request-headers"
---

You can add additional HTTP headers in the request sent to a third\-party origin server during an origin\-pull task. After the configuration is complete, all origin\-pull requests initiated using this domain name carry the configured request header. For more information about origin pull, refer to [Configuring an origin-pull task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-origin-pull-settings).

HTTP request headers are automatically added by a client (such as a browser) when it sends an HTTP request to provide additional information to the server, such as the client type, language, and preferences. For example, you can set the `Accept` field to specify the type of response that the client can accept.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Request header field matching is case insensitive. If a field already exists in the original request header, the new field value overwrites the original field value.</div>


<span id="37a45946"></span>
## Applicable to

Pull streaming domain name

<span id="7372d48b"></span>
## Prerequisites

A domain name has been added

<span id="c7be96cf"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. Find the domain name that you want to view, and click **Settings** in the **Actions** column.

4. Click the **Origin pull** tab.

5. Click **Edit** to the right of the **HTTP request headers** toggle.

6. In the **HTTP request header settings** dialog box that appears, add the request headers as desired.

   * **Parameter**: You can add a maximum of 20 headers. The header name cannot exceed 1024 characters.

   * **Value**: Specify a constant or a variable as the header value.

      * The constant cannot exceed 1024 characters.

      * For variables, you can select a commonly used one from the drop\-down list or manually enter a variable.

         Supported variables include:

      
      |**Variable** |**Description** |**Example value** |
      |---|---|---|
      |$ |Represents the domain name in the origin\-pull request of the client. |example.com |
      |$ |Represents the path of the origin\-pull request excluding the query parameters. If the request is rewritten, this variable represents the rewritten path. |`/dir/sample.php` |
      |$ |Represents the query parameters in the origin\-pull request. If the request is rewritten, this variable represents the rewritten parameters. |`color=red&n=10` |
      |$ |Represents the IP address of the client sending the request. |`10.10.10.10` |
      

7. Click **Confirm**.
