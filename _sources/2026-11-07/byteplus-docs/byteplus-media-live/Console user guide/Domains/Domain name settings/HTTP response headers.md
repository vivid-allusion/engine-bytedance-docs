---
title: "HTTP response headers"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-http-response-headers"
---

You can add additional HTTP headers in the response sent from an edge server to a client. After the configuration is complete, the configured response header parameters are added to the response headers received by all requests sent to this domain name.

The HTTP response header is a series of header fields that the server sends before the response body when it sends an HTTP response. These header fields provide metadata information about the response, such as the status code, content type, cache control, Content\-Encoding, and Content\-Disposition of the response. At the same time, configuring an appropriate HTTP response header can improve security, optimize performance, and improve user experience. It can also help meet compliance requirements and interaction needs for browsers and search engines.

By default, the cache node will pass through the response header of the source station when responding to a user's pull request. You can configure, add, or modify response header parameters through HTTP response header.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Response header field matching is case insensitive. If a field already exists in the original response header, the new field value overwrites the original field value.</div>


<span id="ba3aed7d"></span>
## Applicable to

Pull\-stream domain name

<span id="437cee91"></span>
## Prerequisites

A domain name has been added

<span id="d55ece96"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, click **Domains**.

3. Find the domain name that you want to view, and click **Settings** in the **Actions** column.

4. Click the **Access control** tab.

5. Click **Edit** to the right of the **HTTP response headers** toggle.

6. In the **HTTP response header settings** dialog box that appears, add the response headers as desired.

   * **Parameter**: Select a commonly used header from the drop\-down list or enter a custom one. You can add a maximum of 20 headers. The header name cannot exceed 1024 characters.

      You can select the following parameters from the drop\-down list:

      
      |**Parameter** |**Description** |**Example** |
      |---|---|---|
      |Content\-Type |The type of content returned to the client. |`text/plain` |
      |Cache\-Control |Instructions that control caching behaviors. |`max-age=3600` |
      |Content\-Disposition |The name of the downloaded file returned to the client. |`attachment;filename=Demo.xlsx` |
      |Content\-Language |The language of the content returned to the client. |`zh-CN` |
      |Expires |The expiration time of the response object. |`Wed, 21 Oct 2015 07:28:00 GMT` |
      |Access\-Control\-Allow\-Origin |The sites that can be accessed by cross\-domain requests. |`https://www.another-site.com` |
      |Access\-Control\-Allow\-Headers |The request headers that cross\-origin requests can include. |`X-Custom-Header` |
      |Access\-Control\-Allow\-Methods |The request methods that can be used for cross\-origin requests. |`GET` |
      |Access\-Control\-Max\-Age |How long the results of a preflight request can be cached. |`3600` |
      |Access\-Control\-Expose\-Headers |The response headers that are accessible to clients in cross\-origin requests. |`Content-Encoding`. If you need the client to access more response headers, you can specify them in this field. Multiple response headers are separated by commas (,). |
      

   * **Value**: Specify a constant or a variable as the header value.

      * The constant cannot exceed 1024 characters.

      * For variables, you can select a commonly used one from the drop\-down list or manually enter a variable.

         You can select the following variables from the drop\-down list:

         
         |**Variable** |**Description** |**Example value** |
         |---|---|---|
         |$ |Represents the domain name in the client request. |example.com |
         |$ |Represents the path of the client request excluding the query parameters. If the client request is rewritten, this variable represents the rewritten path. |`/dir/sample.php` |
         |$ |Represents the query parameters in the client request. If the client request is rewritten, this variable represents the rewritten parameters. |`color=red&n=10` |
         |$ |Represents the IP address of the client sending the request. |`10.10.10.10` |
         |$ |Represents the IP address of the edge server responding to the client request. |`10.10.10.10` |
         

7. Click **Confirm**.
