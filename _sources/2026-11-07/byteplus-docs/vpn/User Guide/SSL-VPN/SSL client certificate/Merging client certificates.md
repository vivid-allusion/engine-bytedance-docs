---
title: "Merging client certificates"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Merging-client-certificates"
---

This topic describes how to merge files of an existing .zip SSL client certificate into an .ovpn SSL client certificate.

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios


* If you want to use the downloaded SSL client certificate in `.zip` format for SSL connections on iOS or Android clients. Follow this procedure to merge the four SSL client certificate files locally into one. Merge the certificate into the configuration file. Use the merged client certificate to start your client connection.

* You can also directly download the .ovpn SSL client certificate again from the SSL client certificate console. For specific actions, refer to Downloading an SSL client certificate.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Download the SSL client certificate "certs_vsc\-2feuoxsyxxxxxybovbq.zip" to Local. Specific actions refer to Creating and downloading an SSL client certificate.

2. Use any extraction tool to unzip the client certificate archive certs_vsc\-2feuoxsyxxxxxybovbq.zip. The extracted files are shown in the following figure.

3. Change the format from config.ovpn to config.txt.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We use .txt format here because you may not be able to edit .ovpn files directly. If you can edit .ovpn files directly, skip this step and the final step. This topic covers scenarios where .ovpn files can't be edited directly.   </div>
   


&nbsp;

4. Double\-click the config.txt file and modify the configuration file.

   1. Delete the following lines or add  **#**  at the beginning to comment them out.

      ```Plain Text
      ca ca.crt
      cert client.crt
      key client.key
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1b7e2e1ebbebe409e62388143a09c35c.png) </span>

   2. Rename `ca.crt` to `ca.txt`, then add the content of the `ca.txt` file at the end of the `config.txt` file.

      ```Plain Text
      <ca>
      ca.txt file content
      </ca>
      ```
      

   3. Rename `vsc-im5xxxxxxx9tklp8.crt` to `vsc-im5xxxxxxxx9tklp8.txt`, then add the content of the `vsc-im5xxxxxxxx9tklp8.txt` file at the end of the `config.txt` file.

      ```Plain Text
      <cert>
      vsc-im5xxxxxxxx9tklp8.txt file content
      </cert>
      ```
      

   4. Rename `vsc-im5xxxxxxx9tklp8.key` to `vsc-im5xxxxxxxx9tklp8.txt`, then add the content of the `vsc-im5xxxxxxxx9tklp8.txt` file at the end of the `config.txt` file.

      ```Plain Text
      <key>
      vsc-im5xxxxxxxx9tklp8.txt file content
      </key>
      ```
      

5. Save the modifications and exit. The modified configuration file appears as shown below.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28495bc0c50ed0afd2a34bd3fb8c5995.png) </span>

6. Finally, change the format of the modified `config.txt` file back to the original `config.ovpn`, and use `config.ovpn` to connect.
