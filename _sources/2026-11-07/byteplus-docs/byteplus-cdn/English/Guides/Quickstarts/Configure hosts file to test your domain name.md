---
title: "Configure hosts file to test your domain name"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-test-domain-name-with-hosts"
---

After adding a domain to BytePlus CDN, it is crucial to verify its configuration before updating your public DNS records. This guide provides step\-by\-step instructions on how to modify your local hosts file to point your domain to the CDN, allowing you to safely test access and ensure everything works correctly without affecting your live traffic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Please note that the process of testing CNAME will generate a very small amount of traffic on the CDN side, which will be billed.</div>


* <div data-tips="true" data-tips-type="tip">This document is based on the scenario described in <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview_1">Overview</a>.</div>



<span id="step-1-get-cname"></span>
# Step 1: Get CNAME


1. Log into the [BytePlus CDN Management Console](https://console.byteplus.com/cdn).

2. In the left navigation bar, click on **Domain Names**.

3. On the **Domain Names** page, locate the domain `www.example.com` you added.

4. In the **CNAME** column, click on the **Copy** button.

   The CNAME you obtain should be `www.example.com.bplslb.com`.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a6c418fa763297aaf0b664974c596bb0.png) </span>


<span id="step-2-get-the-ip-address-of-the-cname"></span>
# Step 2: Get the IP address of the CNAME

Follow the steps for your operating system to get the CNAME's IP address.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IP address in the screenshots below is for demonstration purposes only and is not real.</div>


<span id="macos-use-the-dig-command-to-get-the-ip-address"></span>
## macOS: Use the dig command to get the IP address


1. In a Terminal window, run the command `dig www.example.com.bplslb.com`.

2. Under **ANSWER** **SECTION**, find the IP address of the CNAME.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_004df10162659ecc7b86c105e5061295.png) </span>


<span id="windows-use-the-ping-command-to-get-the-ip-address"></span>
## Windows: Use the ping command to get the IP address


1. In a **Command Prompt** window, run the command `ping www.example.com.bplslb.com`.

2. In the command's output, locate the IP address of the CNAME.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c1de146606226ae567cdd4f04d55fd64.png) </span>


<span id="step-3-verify-if-the-ip-address-belongs-to-the-cdn"></span>
# Step 3: Verify if the IP address belongs to the CDN

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this article, assume the IP address you have obtained is <code>203.0.113.5</code>.</div>



1. Open the [Diagnostic Tool](https://console.byteplus.com/cdn/cdn-volc/diagnosis).

2. Enter the obtained IP address and click **Query**.

3. In the query results, check the value in the **Is a CDN Cache Node** column.

* If the value is **Yes**, the IP address is a CDN node, as expected.

* If the value is **No**, it means that the IP address does not belong to the CDN. Please [submit a ticket](https://console.byteplus.com/workorder/create).

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3cf0d782e8ffc1caefb2f7f177407fcf.png) </span>


<span id="step-4-configure-the-hosts-file-of-your-operating-system"></span>
# Step 4: Configure the hosts file of your Operating System

In the hosts file, you need to add an entry to point the domain name of your site to the IP address.

Follow the steps for your operating system to configure the hosts file.

<span id="macos-modify-the-hosts-file"></span>
## macOS: Modify the hosts file


1. In a Terminal window, run the command `sudo nano /etc/hosts`.

2. At the end of the hosts file, enter `203.0.113.5 www.example.com`.

3. Press `CTRL` + `O` to save the file, then press `CTRL` + `X` to exit the editor.

4. To make the changes take effect, run the command `sudo killall -HUP mDNSResponder`.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_580c68beca18fbf7b34c311d4fd06a1d.png) </span>


<span id="windows-modify-the-hosts-file"></span>
## Windows: Modify the hosts file


1. Open Notepad using the **Run as administrator** option.

2. Press `CTRL` + `O`, enter `%Windir%\System32\drivers\etc\hosts` in **File name**, then click **Open**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a14fc1f526ec32b2efa5f3f5e7ee79df.png) </span>

3. At the end of the hosts file, enter `203.0.113.5 www.example.com`.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5025e1778d51d53d116d95b6dc082c22.png) </span>

4. Press `CTRL` + `SHIFT` + `S` to save the changes.

5. To make the changes take effect, open a **Command Prompt** window and run the command `ipconfig /flushdns`.


<span id="step-5-test-your-domain-name"></span>
# Step 5: Test Your Domain Name

Before testing, check that the status of your domain name in the console is Online. If not, please wait a few minutes and then refresh the page to check. If it is still not Online, please [submit a ticket](https://console.byteplus.com/workorder/create).

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b8a160adcd2459d4a2b28136527845a7.png) </span>


1. Use your browser to visit a file on your site. Assume the address of the file is `www.example.com/vip-2_1cbeb77.png`.

2. Press `F12` to open **Developer Tools**.

3. In the file list on the left side of the **Network** tab, find `vip-2_1cbeb77.png` and click on the file.

4. On the **Headers** tab on the right, check that the **Remote Address** is `203.0.113.5`.

* If yes, the test is successful.

* If no, the test is unsuccessful. Please check if the hosts file is configured correctly.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_abd3bbe1441a7551bf08cc605d246878.png) </span>

If the test is successful, please delete the entry you just added in the hosts file. Then, create a CNAME record with your DNS provider. In the CNAME record, point your domain name to `www.example.com.bplslb.com`.
