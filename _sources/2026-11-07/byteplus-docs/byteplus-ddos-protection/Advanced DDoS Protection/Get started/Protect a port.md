---
title: "Protect a port"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-protecting-a-port"
---

To safeguard non\-web services, such as online gaming or e\-commerce activities, you can configure port forwarding rules. This involves replacing your service IP address with that of the Advanced DDoS Protection instance, thus network traffic can be redirected to the scrubbing centers within our global Anycast network for filtering. This document provides a detailed guide on how to configure these port forwarding rules.

<span id="8181c1fb"></span>
## Before you begin

Create an instance of BytePlus Advanced DDoS Protection.

<span id="1bf31a79"></span>
## Precautions

If the domain name of your origin server is non\-existent or unresolvable, the configuration may fail to take effect, or the requests to your origin server may not be forwarded properly.

<span id="92c5881f"></span>
## Procedure

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1NjVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgNTY1IDY1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAxNTIgMzIgTCAyMDUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwN2ZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMTAuODggMzIgTCAyMDMuODggMzUuNSBMIDIwNS42MyAzMiBMIDIwMy44OCAyOC41IFoiIGZpbGw9IiMwMDdmZmYiIHN0cm9rZT0iIzAwN2ZmZiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE1MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjMDA3ZmZmIiBzdHJva2U9IiMwMDdmZmYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BZGRpbmcgYSBmb3J3YXJkaW5nIHJ1bGU8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzUyIDMyIEwgNDA1LjYzIDMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDdmZmYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDEwLjg4IDMyIEwgNDAzLjg4IDM1LjUgTCA0MDUuNjMgMzIgTCA0MDMuODggMjguNSBaIiBmaWxsPSIjMDA3ZmZmIiBzdHJva2U9IiMwMDdmZmYiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIxMiIgeT0iMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjMDA3ZmZmIiBzdHJva2U9IiMwMDdmZmYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogMjEzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTZweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICNGRkZGRkY7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFkZGluZyBiYWNrLXRvLW9yaWdpbiBDSURSIGJsb2NrcyB0byB0aGUgYWxsb3dsaXN0PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0MTIiIHk9IjIiIHdpZHRoPSIxNTAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iIzAwN2ZmZiIgc3Ryb2tlPSIjMDA3ZmZmIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDQxM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDE2cHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjRkZGRkZGOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DaGFuZ2luZyB0aGUgSVAgYWRkcmVzcyBvZiBvcmlnaW4gc2VydmVyPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" width="565px" />

<span id="2a8c1e9b"></span>
## Step 1. Add one or more port forwarding rules


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Provisioning**.

3. Choose **Port config** tab, and select the instance you want to configure.

4. Click **Add forwarding rules**.

5. Choose **Add single rule** or **Add multiple rules in batches**, and configure the parameters.

   * **Add single rule**: Add a rule for one port at a time.

      
      |**Configuration** |**Description** |
      |---|---|
      |Forwarding protocol |Supported protocols are TCP and UDP. |
      |Forwarding port |* The port of Advanced DDoS Protection for forwarding requests. This port should ideally be the same as the origin server port.<br><br>* Within the same Advanced DDoS Protection instance, the forwarding port for each type of forwarding protocol must be unique. |
      |Origin server port |The port of the origin server. |
      |Origin server address |Specify the origin server's IP address or domain name. For load balancing purposes, multiple IP addresses or domain names can be entered simultaneously. However, do not mix IP addresses and domain names in a single rule.<br><br><br>* ✅Example 1. IP addresses<br><br>   ```JSON```<br>```   1.1.1.1```<br>```   1.1.1.2```<br>```   1.1.1.3```<br>```   ```<br>   <br><br>* ✅Example 2. Domain names<br><br>   ```JSON```<br>```   www.test1.com```<br>```   www.test2.com```<br>```   www.test3.com```<br>```   ```<br>   <br><br>* ❌Example 3. An IP address and a domain name<br><br>   ```JSON```<br>```   1.1.1.1```<br>```   www.test2.com```<br>```   ```<br>    |
      

   * **Add multiple rules in batches**: Add rules for multiple ports at once.

      * Enter multiple rules simultaneously, separating each rule by pressing the Enter key.

      * The rule format should be as follows: `protocol_forwarding port_origin server port_origin server address`. Use spaces to separate parameters.

      * Below is a valid example.

         ```JSON
         tcp 1234 1234 1.1.1.1
         udp 1234 1234 www.test.com www.test2.com
         ```
         


<span id="528954e0"></span>
## Step 2. View back\-to\-origin CIDR blocks and add them to the allowlist

When you protect your service with Advanced DDoS Protection, all requests will be redirected to your origin server via the fixed and limited back\-to\-origin CIDR blocks of the Advanced DDoS Protection instance. Consequently, the volume of requests from each back\-to\-origin IP may increase, potentially leading to blocking or rate limiting due to security policies. Therefore, it is essential to allow requests from our back\-to\-origin CIDR blocks.

If the origin server employs a firewall or security software, it is recommended to add the back\-to\-origin CIDR blocks to the allowlist of the firewall, access control list (ACL), or any other security software. This action ensures that your security policies do not block the back\-to\-origin IP addresses.


1. View the CIDR blocks. Below are two methods for viewing CIDR blocks.

   * The CIDR blocks are displayed after clicking **Save** when adding forwarding rules.

   * Go to the **Port config** page and click **View back\-to\-origin CIDR blocks**.

2. Click **Copy all**.

3. Add all the CIDR blocks to the allowlist of the firewall, access control list (ACL), or any other security software.


<span id="3733d726"></span>
## Step 3. Change the IP address of your service

Replace your service's IP address with the one provided by the Advanced DDoS Protection instance. Once the change takes effect, traffic is rerouted to the instance, where it is cleaned and filtered before being forwarded to the origin server. The method to replace the IP address varies based on your platform.

There are two methods to check the IP address of an instance.


* The IP address of the instance is displayed after clicking **Save** when adding forwarding rules.

* Go to the **Instance list** page and view the IP address of your instance.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">If your service uses a domain name, update its A record with your DNS provider to point to the IP address of the Advanced DDoS Protection instance.</div>


<span id="a6a66433"></span>
## What to do next

After configuring the rules, we recommend verifying that they are working correctly. This verification step helps prevent service interruptions caused by incorrect rule configurations.
