---
title: "Modifying an SSL-VPN client certificate"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/modify-the-ssl-client-certificate"
---

In this topic, OpenVPN Connect is used as the SSL\-VPN client to connect Windows, Mac, and iOS clients. If you use another SSL\-VPN client for connection, the downloaded SSL\-VPN client certificate may be incompatible. You can follow the procedure to modify the SSL\-VPN client certificate.

<span id="Pritunl"></span>
## Pritunl

If you use Pritunl for SSL\-VPN connection on your client, you need to perform the following modifications after [downloading an SSL-VPN client certificate](https://docs.byteplus.com/en/docs/vpn/Downloading-an-SSL-client-certificate). Then use the certificate to connect to the SSL\-VPN client.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The downloaded SSL\-VPN client certificate is in <code>.ovpn</code> format. Open the certificate directly and modify it.</div>


* <div data-tips="true" data-tips-type="tip">The downloaded SSL\-VPN client certificate is in <code>.zip</code> format. Extract the ZIP file, open the <code>config.ovpn</code> file, and modify its content.</div>


1. Delete the content in the SSL\-VPN client certificate that Pritunl cannot recognize: `;compress lzo` and `;explicit-exit-notify`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4b0c3f6029f306b5e5199081602b9204.png) </span>

2. Add `SSL-VPNserver protocol type -client` at the end of the fourth line in the SSL\-VPN client certificate.

   * **Before adding**

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_209bb05197b676cb399ac4d66f5f7fd4.png) </span>

   * **Post\-modification**

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_53e76a31ccf973b5761953f5369f4ef7.png) </span>
