---
title: "Using the HMAC plugin for AK/SK authentication"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Using_the_HMAC_plugin_for_AKSK_authentication"
---

The HMAC plugin implements tamper\-proof signature generation for HTTP requests based on the HMAC algorithm and identity authentication based on the signature. This article explains how to use the HMAC plugin.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The HMAC plugin supports being turned on and off at the instance, service, and route levels, with the priority of configuration effectiveness being route \> service \> instance.

* Once HMAC is enabled, only signatures made with valid consumers' AK/SK can pass the authentication and authorization.

* AK/SK is generated within the consumer, and a consumer can have at most one AK/SK.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65raI6LS56ICF"></span>
### Step 1: Create a consumer


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **consumer management \> consumer list ** .

4. On the consumer page, click **create consumer ** .

5. On the **create consumer** page, complete the following settings, then click **Confirm**.

   
   |parameter |Description |sample value |
   |---|---|---|
   |Instance |Select the instance to which the consumer belongs. |instance\-doc |
   |Consumer name |Custom consumer name to identify the consumer. |Consumer\-doc |
   |Notes/comments |Optional. You can choose whether to edit the notes/comments as needed for your business, e.g., the purpose of the consumer, to facilitate later identification. |none |
   


<span id=".5q2l6aqk5LqM77ya5raI6LS56ICF55Sf5oiQIEFLL1NL"></span>
### Step 2: Consumer generates AK/SK


1. In the consumer list, click the target consumer name to go to the consumer details page.

2. In the credential region, click **Generate** **AK/SK**。

3. In credentials, you can view the generated AK/SK.


<span id=".5q2l6aqk5LiJ77ya5a6i5oi356uv55Sf5oiQ562-5ZCN"></span>
### Step 3: Client Generates Signature


1. Extract key data from the original request to obtain a string used for signing `stringToSign`.

   Field extraction content and rule description:

   
   |Field name. |Cannot be empty |Field value when empty' |Description |
   |---|---|---|---|
   |HTTPMethod |No |POST |The methods of HTTP, all in uppercase, such as POST. |
   |Accept |Yes |\n |The value of the Accept header in the request suggests to use Display settings for the Accept Header. Some HTTP clients may default the Accept setting to \*/\* causing signature failure. |
   |Content\-MD5 |Yes |\n |When the request has a Body and it is not in Form style, calculate the Content\-MD5 header, which can be empty.<br><br>Generation method:<br><br>```java```<br>```String content-MD5 = Base64.encodeBase64(MD5(bodyStream.getbytes("UTF-8")));```<br> |
   |Content\-Type |Yes |\n |The value of the Content\-Type header in the request. |
   |Date |Yes |\n |The value of the Date header in the request, which can be empty. |
   |Headers |Yes |No need to add \n' |* select specified headers to participate in signature<br><br>   * Assembly method:<br><br>      ```http```<br>```      HeaderKey1 + ":" + HeaderValue1 + "\n"\+```<br>```      HeaderKey2 + ":" + HeaderValue2 + "\n"\+```<br>```      ...```<br>```      HeaderKeyN + ":" + HeaderValueN + "\n"```<br>```      ```<br>      <br><br>   * If HeaderValue is empty, retain HeaderKey, and the signature content is as follows:<br><br>      ```http```<br>```      HeaderKey1 + ":" + "\n"```<br>```      ```<br>      <br><br>   * All Header Keys that participate in the signing are separated by commas and placed in the Header with Key `X-Ca-Signature-Headers`, as follows:<br><br>      ```http```<br>```      x-apig-ca-signature-headers: Headerkey1, HeaderKey2, HeaderKey3```<br>```      ```<br>      <br><br>* The following Headers do not participate in the Header signature calculation<br><br>   * X\-apig\-ca\-signature<br><br>   * X\-apig\-ca\-signature\-headers<br><br>   * Accept<br><br>   * Content\-MD5<br><br>   * Content\-Type<br><br>   * Date |
   |PathAndParameters |Yes |\n |It includes all parameters from Path, Query, and Form, presented as follows:<br><br>```http```<br>```Path + "?" + Key1 + "=" + Value1 + "&" + Key2 + "=" + Value2 + ... "&" + KeyN + "=" + ValueN```<br><br><br><br>* After dictionary ordering the Query and Form parameters by Key, concatenate using the method above.<br><br>* When Query and Form parameters are empty, use Path directly without adding anything.<br><br>* When the Value of a parameter is empty, only retain the Key for the signature, as follows:<br><br>   ```http```<br>```   Path + "?" + Key1```<br>```   ```<br>   <br><br>* When Query and Form contain array parameters (parameters with the same key but different values), use the first Value for signature calculation. |
   

   3. View the original request.

      Sample of the original request is as shown:

      ```html
      POST/hmactest/test?param1=querystringcontent HTTP/1.1
      host:example.apig.com
      accept:application/json; charset=utf-8
      
      content-type:application/x-www-form-urlencoded; charset=utf-8
      date:Wed, 02 May 2022 12:30:56 GMT+00:00
      X-Top-Account-Id: 20*****346'
      X-Top-Request-Id: 02********415**********000********1b6********8*****d4
      X-Top-Region: cn-north-2
      content-length:33
      
      username=test&password=test1234
      ```
      

   4. Extract key data from the original request.

      ```html
      HTTPMethod：POST
      Accept：application/json; charset=utf-8
      Content-MD5 ：
      Content-Type：application/x-www-form-urlencoded; charset=utf-8
      Date：Wed, 02 May 2022 12:30:56 GMT+00:00
      Headers：
      PathAndParameters：
      ```
      

   5. Compose the signature string `stringToSign`.

   The string is case\-sensitive and fields are separated by \n.

2. Use the encryption algorithm and `consumerSK from the consumer` to encrypt the extracted `signature string stringToSign` to get the `signature sign`.

   The calculation method is as follows:

   ```java
   Mac hmacSha256 = Mac.getInstance("HmacSHA256");
   byte[] secretBytes = consumerSK.getBytes("UTF-8");
   hmacSha256.init(new SecretKeySpec(secretBytes,0, secretBytes.length, "HmacSHA256"));
   byte[] result = hmacSha256.doFinal(stringToSign.getBytes("UTF-8"));
   String sign = Base64.encodeBase64String(result);
   ```
   

   After the encryption process, an example of the obtained `signature sign` is as follows:

   ```xml
   POST
   application/json; charset=utf-8
   
   application/x-www-form-urlencoded; charset=utf-8
    Wed, 02 May 2022 12:30:56 GMT+00:00
   X-Top-Account-Id:20*****346
   X-Top-Request-Id:02********415**********000********1b6********8*****d4
   X-Top-Region:cn-north-2
   /hmactest/test?param1=querystringcontent&username=test&password=test1234
   ```
   

3. Add all headers related to the signature into the original HTTP request to get the final HTTP request.

   ```xml
   POST/hmactest/test?param1=querystringcontent HTTP/1.1
   host:example.apig.com
   accept:application/json; charset=utf-8
   
   content-type:application/x-www-form-urlencoded; charset=utf-8
   date:Wed, 02 May 2022 12:30:56 GMT+00:00
   X-Top-Account-Id: 20*****346'
   X-Top-Request-Id: 02********415**********000********1b6********8*****d4
   X-Top-Region: cn-north-2
   x-apig-ca-key: consumer's AK'
   x-apig-ca-signature-method: HmacSHA256
   x-apig-ca-signature-headers: X-Top-Account-Id,X-Top-Request-Id,X-Top-Region
   x-apig-ca-signature: signature calculation result'
   content-length:33
   
   username=test&password=test1234
   ```
   

   Headers newly added to the request and their description:

   
   |header content |Description |
   |---|---|
   |x\-apig\-ca\-key |User's AK |
   |x\-apig\-ca\-signature\-method |HmacSHA256 |
   |x\-apig\-ca\-signature\-headers |X\-Top\-Account\-Id,X\-Top\-Request\-Id,X\-Top\-Region |
   |x\-apig\-ca\-signature |Signature calculation result |
   


<span id=".5q2l6aqk5Zub77ya5pyN5Yqh56uv6aqM6K-B562-5ZCN"></span>
### Step 4: The server verifies the signature


1. Extract the consistent string `stringToSign` from the received request for signing.

2. Read `consumerAK` from the received request and query the corresponding `consumerSK through consumerAK`.

3. Use the encryption algorithm and corresponding `consumerSK` to encrypt the critical data signature string and obtain the signature.

4. Read the client's signature from the received request, and compare the consistency of the server\-side and client\-side signatures.
