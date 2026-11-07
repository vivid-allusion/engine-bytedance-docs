---
title: "Protect a website"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-protecting-a-website"
---

To protect your website from DDoS attacks, you need to add your domain to BytePlus Advanced DDoS Protection and update its DNS record. This process reroutes your traffic through our global scrubbing centers, which filter out malicious requests before forwarding legitimate traffic to your origin server. This guide provides step\-by\-step instructions for provisioning your website, ensuring its security and improving response speed.

<span id="56c97d25"></span>
## Before you begin

Create an instance of BytePlus Advanced DDoS Protection.

<span id="1efde513"></span>
## Precautions

Both WebSocket and WebSockets protocols are supported and enabled by default.

<span id="ec056559"></span>
## Procedure

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI5MDVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgOTA1IDY1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAxNDIgMzIgTCAxODUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwN2ZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxOTAuODggMzIgTCAxODMuODggMzUuNSBMIDE4NS42MyAzMiBMIDE4My44OCAyOC41IFoiIGZpbGw9IiMwMDdmZmYiIHN0cm9rZT0iIzAwN2ZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjMDA3ZmZmIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BZGRpbmcgYSBkb21haW4gbmFtZTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMzIgMzIgTCAzNzUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwN2ZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAzODAuODggMzIgTCAzNzMuODggMzUuNSBMIDM3NS42MyAzMiBMIDM3My44OCAyOC41IFoiIGZpbGw9IiMwMDdmZmYiIHN0cm9rZT0iIzAwN2ZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTkyIiB5PSIyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiMwMDdmZmYiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAxOTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxNnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogI0ZGRkZGRjsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QWRkaW5nIGJhY2stdG8tb3JpZ2luIENJRFIgYmxvY2tzIHRvIHRoZSBhbGxvd2xpc3Q8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTIyIDMyIEwgNTQyIDMyIEwgNTY1LjYzIDMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDdmZmYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTcwLjg4IDMyIEwgNTYzLjg4IDM1LjUgTCA1NjUuNjMgMzIgTCA1NjMuODggMjguNSBaIiBmaWxsPSIjMDA3ZmZmIiBzdHJva2U9IiMwMDdmZmYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM4MiIgeT0iMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjMDA3ZmZmIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogMzgzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICNGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNvbmZpcm1pbmcgZm9yd2FyZGluZyBjb25maWd1cmF0aW9uPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDcxMiAzMiBMIDc1NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDA3ZmZmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc2MC44OCAzMiBMIDc1My44OCAzNS41IEwgNzU1LjYzIDMyIEwgNzUzLjg4IDI4LjUgWiIgZmlsbD0iIzAwN2ZmZiIgc3Ryb2tlPSIjMDA3ZmZmIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI1NzIiIHk9IjIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iIzY2YjJmZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDU3M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj4oT3B0aW9uYWwpPGJyIC8+QWRkaW5nIGFuIEhUVFBTIGNlcnRpZmljYXRlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NjIiIHk9IjIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iIzAwN2ZmZiIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDc2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Db25maWd1cmluZyBhIEROUyByZWNvcmQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" width="905px" />

<span id="9d75ae36"></span>
## Step 1. Adding one or more domain names


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Provisioning**.

3. Choose the **Website config** tab, and click **Add domain name**.

4. Configure the parameters.

   
   |**Configuration** |**Description** |
   |---|---|
   |**Provisioning** ||
   |**Associated instance** |Select the associated instance to protect your website services.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 10 instances can be selected at a time.</div><br> |
   |**Domain name** |Enter the domain name of your website. Both wildcard domain names and exact\-match domain names are supported.<br><br><br>* To include both a wildcard domain name and its primary domain name, you must enter them individually. For example, to secure both `*.a.com` and `a.com`, you must add each domain name separately.<br><br>* If a wildcard domain name and its corresponding exact\-match domain name are concurrently configured, the Advanced DDoS Protection instance will prioritize the matching of forwarding rules and protection policies for the exact\-match domain. To illustrate, if both `*.a.com` and `www.a.com` are provisioned, the forwarding rules and protection policies for `www.a.com` will take precedence. |
   |**Protocol type** |Select the communication protocol used by your websites, and enter available ports ranging from 1 to 65534. Currently, both HTTP and HTTPS protocols are supported.<br><br><br>* **HTTP**: When HTTP is selected, port 80 will be used by default, but this can be modified. The WebSocket protocol will be also automatically enabled.<br><br>* **HTTPS**: When HTTPS is selected, port 443 will be used by default, but this can be modified. The WebSocket protocol will be also automatically enabled.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To ensure proper forwarding, you must add an SSL certificate if you select <strong>HTTPS</strong>. For more details, see <a href="https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-setting-an-SSL-certificate-for-domain-name">Setting an SSL certificate for domain name</a>.   </div><br>   <br><br>   * **HTTPS redirection**: When HTTPS is enabled and HTTP is disabled, the system automatically activates HTTPS redirection. This function redirects all HTTP requests to HTTPS requests on the standard port 443. If this feature is turned off, the system will discard all HTTP requests.<br><br>   * **Advanced settings**: If HTTPS is selected, you can click **Expand advanced settings** to configure **Protocol following** and **HTTP/2**.<br><br>      * **Protocol following**: When you select both HTTP and HTTPS, you can enable **Protocol following**. This ensures that back\-to\-origin requests are forwarded using the same protocol as the access protocol. To ensure smooth transmission, verify that the origin server supports both HTTP and HTTPS protocols.<br><br>      * **HTTP/2**: HTTP/2 is enabled by default and cannot be deactivated when HTTPS is selected. Once enabled, it provides access protection under the HTTP/2 protocol and requests are forwarded to the origin server using either HTTP 1.0 or HTTP 1.1. |
   |**Back\-to\-origin configuration** ||
   |**Load balancing algorithm** |The Source Address Hash (SH) is selected by default and cannot be modified. This algorithm operates based on the consistent hashing of the source IP address. Consequently, requests originating from the same source IP address are consistently directed to the same backend server. |
   |**Origin server type** |Set the type of your origin server.<br><br><br>* Source IP: Use IP addresses to identify different origin servers.<br><br>* Source domain name: Use domain names to identify different origin servers. |
   |**Origin server configuration** |Click **Add origin server address**, and configure the related parameters.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="default">Up to 20 origin servers can be added.</div><br><br><br><br>* **Back\-to\-origin protocol**: The protocol from the Advanced DDoS Protection instance to the origin server. HTTP and HTTPS are supported. If you have enabled **Protocol following** for the domain, you must select both HTTP and HTTPS as the back\-to\-origin protocols for the feature to work correctly.<br><br>* **Origin server address**: Specify the IP address or domain name of the origin server. The address you enter must match the selected **Origin server type** (an IP address for **Source IP**, or a domain name for **Source domain name**).<br><br>* **Origin server port**: The port of your origin server.<br><br>* **Weight**: This value determines the proportion of requests that the origin server receives. This proportion is calculated by dividing the weight of the origin server by the total weight of all servers in the group. The value can be configured within a range of 1 to 99, and it is set as 99 by default.<br><br>* **Action**: To remove an unneeded item, click the **Delete** icon. |
   

5. Click **Next Step**.

   You can view CIDR blocks of the Advanced DDoS Protection on the page.


<span id="c8e9958a"></span>
## Step 2. Adding back\-to\-origin CIDR blocks to the allowlist

After you provision your service, Advanced DDoS Protection redirects all requests to your origin server. This traffic comes from a fixed set of back\-to\-origin CIDR blocks. Consequently, the request volume allocated to each back\-to\-origin IP may increase, potentially leading to blocking or rate limiting due to security policies. Therefore, it is essential to allow requests from our back\-to\-origin CIDR blocks.

If your origin server uses a firewall or other security software, add the back\-to\-origin CIDR blocks to its allowlist or access control list (ACL). This action prevents security policies from blocking the back\-to\-origin IP addresses.


1. View the CIDR blocks. Below are two methods for viewing CIDR blocks.

   * The CIDR blocks are displayed after clicking **Save** when adding forwarding rules.

   * Go to the **Port config** page, and click **View back\-to\-origin CIDR blocks**.

2. Click **Copy all.** 

3. Add all the CIDR blocks to the allowlist of the firewall, access control list (ACL), or any other security software.


<span id="e00ad19d"></span>
## Step 3. Confirming your forwarding configuration

In this step, verify your configurations and view back\-to\-origin CIDR blocks. Additionally, you have the option to copy the domain name, port number, and CIDR blocks.


* Ensure all information is correctly configured before clicking **Save**.

* To make changes to your configuration, click **Previous step** to return to the editing stage.


Once the domain name configuration has been confirmed, the Advanced DDoS Protection IP address and CNAME record will be shown on the page. Or you can go to the **Instance list** to view more details.

<span id="04f16c6a"></span>
## (Optional) Step 4. Adding an SSL certificate if HTTPS protocol is selected

If the HTTPS protocol is selected when adding domain names, a certificate must be set up to ensure the normal forwarding of HTTPS requests. However, if you add domain names with only HTTP protocol configured, you can just skip this step.


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Provisioning**.

3. Choose the **Website config** tab, and click the edit icon of the domain name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aae051f16d614a1b98cf7eff9bb33e2e~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Upload a new certificate if you do not have a certificate to add. For more details, see <a href="https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-uploading-an-ssl-certificate">Uploading an SSL certificate</a>.   </div>
   

4. Select a certificate or upload a new one.

5. Click **OK**.


<span id="1c76cd90"></span>
## Step 5. Configuring a DNS record for your domain name

You can proceed to the DNS resolution provider, and add a CNAME record for the website to be protected. This process will route the service traffic to Advanced DDoS Protection, thereby safeguarding it from potential DDoS attacks.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Before setting the DNS record, make sure that an SSL certificate is set for your website if HTTPS protocol is selected.</div>


<span id="ccc710ee"></span>
## What to do next

We recommend verifying that the forwarding settings work correctly after configuration. This verification helps prevent service interruptions caused by incorrect forwarding configurations. For more details, see [Verifying forwarding configurations](https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-verifying-the-forwarding-configurations).
