---
title: "Configure instance public network access"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access"
---

The BytePlus Cloud Search instance supports enabling public network access, allowing devices outside the VPC to access the instance. When devices outside the VPC no longer need to access the Cloud Search instance, you must promptly disable public network access. This topic explains how to configure instance public network access.

<span id="bf98cccc"></span>
## Precautions


* To enable public network access for the instance, you need to associate an existing Elastic IP (EIP). Charges are billed by EIP. For more information, see [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

* Monitor the expiration time of the EIP. If it expires without renewal, the public domain name will become unavailable.

* When public network access is enabled for a Cloud Search instance, the IP allowlist automatically includes `127.0.0.1`, blocking all public IPs from accessing it. To use normally, modify the IP allowlist configuration when enabling public network access.


<span id="cec1b3d8"></span>
## Enable public network access


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. In the left navigation bar, select **Basic information**, then turn on the **Public network access** switch in the **Instance access information** area.

5. On the **Enable public network access** panel, complete the following steps, then click **OK**.

   1. Select the Elastic IP (EIP) to associate. If no EIP is available, see [Apply for EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).

   2. Configure the IP allowlist for public network access.

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Description      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">When configuring the IP allowlist, you can specify a single IP address or an IP network segment. Please follow the format requirements below:      </div>
      

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">IP address format: Must be a valid IPv4 address consisting of four integers from 0 to 255, separated by periods (.).      </div>
      

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">CIDR segment: Must be in standard format, with the IP and mask matching.      </div>
      

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The IP part must be the network address, the first address in the subnet; all host bits must be zero.      </div>
      

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The network prefix length range is 0~32. <code>/0</code> is valid, representing the entire IPv4 address space (<code>0.0.0.0/0</code>); <code>/32</code> denotes a single host address.      </div>
      

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Reserved IP ranges such as the loopback address <code>127.0.0.0/8</code> are not allowed.      </div>
      

            * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Configuration with <code>0.0.0.0/x</code> is not allowed.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can click <strong>Add IP allowlist group</strong> to manage IP allowlist groups.      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">      
      |<strong>Examples of valid CIDR notation</strong> |<strong>Examples of invalid CIDR notation</strong> |
      |---|---|
      |* 192.168.0.0/24: correct Class C network address;<br><br>* 10.0.0.0/8: correct Class A network address;<br><br>* 172.16.0.0/12: correct Class B network address. |* 192.168.1.1/24: not a network address (last octet is not 0);<br><br>* 192.168.0.0/33: invalid prefix length (exceeds 32);<br><br>* 256.0.0.0/24: invalid IP address (the first octet exceeds 255);<br><br>* 192.168.01.0/24: incorrect format (leading zero in the third octet). |
            </div>
      

6. Check the progress of enabling public network access for the instance.

   Return to the instances page, and the instance status shows as **Variation**. When the status shows **Running**, it indicates that the association and public network access activation succeeded.


<span id="aed52701"></span>
## Disable public access

After disabling public network access to the instance, clients can no longer access the Cloud Search instance through the original public access address. Confirm your services are not using the public address to avoid unnecessary losses.


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name.

4. In the left navigation bar, select **Basic information**, then click the switch next to **Public network access**.

5. In the pop\-up dialog box, review the precautions for disabling public network access, then click **OK**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After disabling public network access, the disassociated EIP will remain and incur charges. Release the EIP resource on your own.   </div>
