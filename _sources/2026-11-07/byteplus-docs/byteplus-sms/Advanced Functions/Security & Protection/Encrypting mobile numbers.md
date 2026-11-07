---
title: "Encrypting mobile numbers"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-encrypting-mobile-numbers"
---

BytePlus Messaging provides you with the feature of encrypting mobile numbers. The supported encryption methods are RSA2048 and AES256. You can choose the encryption method in the BytePlus Messaging console. After configuration, the mobile numbers in both the sending\-message APIs and their callbacks can be encrypted and decrypted.

<span id="75b42679"></span>
## Prerequisite

You have activated BytePlus Messaging. For details, see [Activating BytePlus Messaging](https://docs.byteplus.com/en/byteplus-sms/docs/activating-byteplus-sms).

<span id="e3898aaf"></span>
## Procedure

Follow the steps below to enable or disable mobile number encryption in the BytePlus console.

<span id="919ca2c4"></span>
### Enabling encryption


1. Go to the [BytePlus Messaging console](https://console.byteplus.com/sms).

2. In the left navigation pane, click **Setting** \> **Service Settings** \> **Product function settings** tab.

3. Click **Configure Now**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebdaae4295164866a5cd9d8178db098a~tplv-goo7wpa0wc-image.image) </span>


4. In the pop\-up window, refer to the description below to fill in the blanks.

   
   |**Field name** |**Description** |
   |---|---|
   |Encryption configuration name |Based on your scenario, fill in your configuration name. The name should be unique and limited to 1\-15 characters and passed in the sending request with a field parameter of `EncryptName`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The name must not duplicate any existing names.</div><br> |
   |Encryption method |Choose your encryption methods:<br><br><br>* AES256<br><br>* RSA2048 |
   |Key generation method |Choose the key generation method that best suits your needs:<br><br><br>* System\-generated: BytePlus automatically generates a key based on the chosen encryption method.<br><br>* Manual input:<br><br>   * For AES256 encryption: Input a 256\-bit key, which must consist only of alphanumeric characters.<br><br>   * For RSA2048 encryption: Input a public\-private key pair not exceeding 2048 bits, supporting alphanumeric characters and special characters. |
   |Whether to add salt |Choose whether to include "salt" in the process. Currently, BytePlus Messaging only supports adding "suffix salt", which means the "salt" is appended to the end of the string by default.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Salting involves inserting a specified string ("salt") at a specific location in the string, disrupting the original string and enhancing security.</div><br> |
   |Salt generation method |If you need to add "salt", you can choose the "salt" generation method according to the actual business needs, and support system generation or direct input:<br><br>Choose either of the following methods to generate the "salt":<br><br><br>* System\-generated.<br><br>* Manual input: Input an 8\-character string which must consist only of alphanumeric characters. |
   

5. Click **OK** to finish your encryption configuration.

   Now you have successfully added an encryption configuration. The encryption will be enabled immediately. You can check its status or copy the generated key on the **Mobile number encryption** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c68640be2d97422d9168ff85ba83efad~tplv-goo7wpa0wc-image.image) </span>


<span id="cdc1eeeb"></span>
### Disabling encryption

On the **Mobile number encryption** page, find the target encryption configuration. In the **Actions** column, click the toggle switch (blue for Enabled, grey for Disabled).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ce16d3205ed47798b97f8e267f56a4b~tplv-goo7wpa0wc-image.image) </span>

After disabling:


* New message\-sending requests will no longer support encryption or decryption.

* Messaging messages that have been sent based on that encryption configuration will still have callbacks processed based on that encryption configuration.


<span id="da61c22c"></span>
### Using encryption and decryption tool

BytePlus Messaging provides you with encryption and decryption tools, allowing you to enter plaintext phone numbers or ciphertext strings to test encryption and decryption functions. The steps are as follows:


1. Go to the [BytePlus Messaging console](https://console.byteplus.com/sms).

2. In the left navigation pane, click **Setting** \> **Service Settings** \> **Product function settings** tab.

3. In the **Mobile number encryption**, find the target configuration. In the **Actions** column, click **Crypto tool**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/baa68715e62c494c816f0cd8c7040db6~tplv-goo7wpa0wc-image.image) </span>


4. On the pop\-up window, you can test encryption and decryption functions based on your target as follows:

   
   |**Target** |**Step** |
   |---|---|
   |Encryption |Enter a plaintext number on the left side of the window and then click **Encrypt**. You will see the ciphertext string encrypted with your configuration on the right side.<br><br>**Note**:<br><br>If you configured the “suffix salt", it will also be automatically added to the end of the phone number and then encrypted. |
   |Decryption |Enter the ciphertext string on the right side and then click **Decrypt**. You will see the decrypted plaintext number with your configuration on the left side. |
   


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6dedc99f4e2437985060e20d94a6888~tplv-goo7wpa0wc-image.image) </span>

<span id="656107b8"></span>
## Related parameters

You can apply your configuration to the sending\-message requests based on the following parameters.

<span id="98ec7d4d"></span>
### Related parameters in the sending request

You must include the following parameters in the sending request to use the encryption feature. For other parameters, see the API reference related to sending Messaging.


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|EncryptName |string |No |The encryption configuration name you filled in the Console. BytePlus Messaging will apply this configuration to decrypt the ciphertext strings before dispatching them. |
|PhoneNumbers |string |Yes |The target phone number(s) for Messaging sending. Can be passed as ciphertext strings. Multiple ciphertext strings should be separated by commas (,). |


<span id="9f323901"></span>
### Related parameters in the callback function

If you include an encryption configuration in the sending request, the `mobile` field in the callback message will contain the ciphertext string resulting from encrypting the plain mobile number based on the provided encryption configuration. The relevant fields are listed below.


|**Parameter** |**Type** |**Description** |
|---|---|---|
|mobile |string |Mobile number or ciphertext string. |
|EncryptName |string |The encryption configuration name, consistent with the encryption configuration in the sending request. |
