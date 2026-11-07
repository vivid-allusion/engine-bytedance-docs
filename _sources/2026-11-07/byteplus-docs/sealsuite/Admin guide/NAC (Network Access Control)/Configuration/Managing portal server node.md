---
title: "Managing portal server node"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-guest-portal-server"
---

The SealSuite RADIUS server has a built\-in Portal authentication service, which listens on TCP port 9100. When your network device needs to perform handshake communication with an external server through a specific Portal protocol (v1/v2), you need to configure Portal Server nodes in the SealSuite Admin Console.

<span id="70811dae"></span>
# Prerequisites

Before you begin, make sure the following requirements are met:


* A RADIUS server has been added. For details, see [Adding a RADIUS server](https://docs.byteplus.com/docs/sealsuite/docs-adding-a-radius-server).

* Portal authentication configurations based on an external server have been completed on the network device, such as the AC or switch, according to the vendor specifications. The shared key, protocol version, and communication port parameters used for integration with SealSuite have also been preset.


<span id="b46ce138"></span>
# Add a Portal Server

<span id="27068717"></span>
## Configuration Entry

You can go to the Portal Server configuration page through either of the following paths:


* **Entry 1**: Go to **NAC \> Config**, click the **Portal Server** tab, and click  **+ Add Now** to add a server.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/734cd24a9e134d6b8049d751bd6c065c~tplv-goo7wpa0wc-image.image) </span>

* **Entry 2**: On the **General** tab of the **RADIUS Server** details page, find the **Advanced settings** area and click **Configure**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51f1342a954c4dadbda8ea81fb6b6535~tplv-goo7wpa0wc-image.image) </span>


<span id="837f5d60"></span>
## Configuration Parameters

After entering the configuration page, align the following parameters according to the manual requirements of your network hardware:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f8ce8c1608243d39df6e623dc920a79~tplv-goo7wpa0wc-image.image) </span>


|**Configuration Item** |**Description** |
|---|---|
|**Portal authentication service name** |Custom name used to identify the Portal authentication service, such as `HQ-Huawei-AC`. |
|**Select RADIUS gateway** |Select the RADIUS gateway that hosts the Portal authentication service. The Portal service runs on the IP address of this gateway. This configuration determines which IP address the network device should initiate protocol handshakes and heartbeats to. |
|**Wireless controller docking address** |Enter the communication IP address and port of the wireless controller. Example format: `192.168.1.1:2000`. SealSuite sends authorization instructions to this address. |
|**Portal server port** |The HTTP port listened on by the built\-in Portal service of the RADIUS gateway. If there are no special configuration requirements, keep the default port `9100`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This port must be allowed through the firewall. User mobile phones or computers access the H5 authentication page and submit QR code or account information through this port.</div><br> |
|**Portal protocol port** |Used for Portal protocol interaction between SealSuite and the network device, including receiving and sending protocol packets. If there are no special configuration requirements, keep the default port `50100`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">UDP must be allowed through the firewall. If this port is unreachable, the hardware considers the Portal Server offline and refuses to redirect users.</div><br> |
|**Portal protocol version** |Options include **v1** and **v2**. Check the supported version on the network device side. A version mismatch will cause protocol parsing failures, which may appear as no response or an error on the page after the user submits information. |
|**Protocol type** |Determines the encryption method used during credential transmission. Options include **PAP** and **CHAP**. This must be strictly consistent with the hardware\-side configuration. |
|**Re\-direct page for successful authentication** |The destination URL that the browser automatically redirects to after employee or visitor authentication succeeds. For example, you can configure this as the enterprise official website homepage or intranet portal. |
|**Re\-direct page for failed authentication** |The destination URL that the browser automatically redirects to after employee or visitor authentication fails. It is recommended to configure this as an internal network access troubleshooting guide page, so that employees or visitors can obtain IT assistance when authentication fails. |
|**User IP name** |The default value is `userip`. SealSuite uses this field to identify the IP address of the endpoint currently performing the operation. If this does not match the parameter name defined on the hardware side, SealSuite cannot identify the endpoint to be released. |
|**Wireless controller IP field name** |The default value is `nasip`. This field is used to reversely parse which wireless controller initiated the request from the URL. When multiple wireless controllers exist, this field ensures that SealSuite can send authorization instructions back to the correct hardware device. It has higher priority than the configuration in **Wireless controller docking address**. |


<span id="5e958b6f"></span>
# Edit or Delete a Portal Server

On the **Portal Server** tab, you can manage created Portal Servers. Note the following:


* **Edit with caution**: Modifying the protocol version, key, or port will directly invalidate ongoing Portal authentication. It is recommended to make adjustments during off\-peak hours.

* **Deletion impact**: After a Portal Server node is deleted, all employees and visitors that depend on this protocol channel will be unable to open the authentication page or complete authorization.

* **CoA linkage**: To immediately disconnect users when “Disable Account” is performed in the backend, make sure the CoA port is also enabled on the network device side.
