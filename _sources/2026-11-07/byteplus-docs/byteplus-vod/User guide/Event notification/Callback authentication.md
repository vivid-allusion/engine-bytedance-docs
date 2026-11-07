---
title: "Callback authentication"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-callback-authentication"
---

To secure your HTTP callback endpoint and prevent invalid requests, you can implement callback authentication. This guide explains the signature\-based authentication mechanism used by BytePlus VOD, details the validation flow for your receiving server, and provides code examples in Go, Python, Java, and PHP to help you get started quickly.

<span id="b7e8d68f"></span>
## Authentication mechanism

BytePlus VOD supports adding custom signature headers in HTTP/HTTPS callbacks. These headers enable the receiving server to authenticate the requests and prevent any illegal or invalid requests. BytePlus VOD recommends that you enable HTTP callback authentication, but this is optional.

If you enable callback authentication and set an authentication key, the callback will include all information needed for authentication by the receiving server.

<span id="08512904"></span>
### Authentication parameters

The following authentication parameters can be added to the callback headers.


|Field |Description |
|---|---|
|X\-VOD\-TIMESTAMP |The time when the callback request was initiated. A Unix timestamp in seconds. |
|X\-VOD\-SIGNATURE |The signature string, a 32\-character hexadecimal MD5 hash. See [Signature calculation](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-authentication#9f50de9a). |


<span id="9f50de9a"></span>
### Signature calculation

`X-VOD-SIGNATURE` relies on the following fields:


|Field |Description |Example |
|---|---|---|
|Callback URL |The callback URL that you configured in the BytePlus VOD console. |https://www.example1.com/your/callback |
|X\-VOD\-TIMESTAMP |The time when the callback request was initiated. A Unix timestamp in seconds. |1545675780 |
|PrivateKey |The authentication key you set in the BytePlus VOD console. |ABCDabcd1234 |
|CallbackDataJsonBase64Encode |Base64\-encoded callback data.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Do not remove the spaces.</div><br> |ewoiYSI6MSwKImIiOjIKfQ== |


You can concatenate the above four fields in order, separated by a vertical bar (`|`), and then calculate the MD5 value. An example is shown below:

```Plain
CallbackContent = base64Encode(CallbackDataJson)
MD5Content = CallbackURL|X-VOD-TIMESTAMP|PrivateKey|CallbackContent
X-VOD-SIGNATURE = md5sum(MD5Content)
```


<span id="cf8bbb4c"></span>
## The validation flow of the receiving server


1. The receiving server receives the callback JSON and encodes it with Base64.

2. The receiving server concatenates the callback URL, the X\-VOD\-TIMESTAMP value, the PrivateKey, and the Base64\-encoded callback JSON. It then calculates the MD5 hash of this string and compares the result with the X\-VOD\-SIGNATURE value from the request. The request is considered invalid if the signatures do not match.

3. (Optional) The receiving server obtains the current time and subtracts the X\-VOD\-TIMESTAMP value from the current time. The request is invalid if the time calculated exceeds the specific duration set by the server (for example, 8 minutes).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The server can decide whether or not to verify time difference errors caused by time settings and other issues.   </div>
   

<span id="93000103"></span>
## Receiving server examples

BytePlus VOD offers callback authentication examples for Go, Python, Java, and PHP.


<Tabs>
<Tab zoneid="zHhi8ZpFmR" title="Go">
<TabTitle>Go</TabTitle>

Go demo:

```Go
func Callback(r *http.Request) {
   timestamp := r.Header.Get("X-VOD-TIMESTAMP")
   // Verify X-VOD-TIMESTAMP
   tm, _ := strconv.ParseInt(timestamp, 10, 64)
   if time.Now().Unix() - tm > consts.MaxRequestTime {
       // Signature verification fails if it exceeds the specified time range
   }
   // Base64 encode the request body
   body, _ := io.ReadAll(r.Body)
   callbackContent := base64.StdEncoding.EncodeToString(body)
   // Concatenate the signature content using vertical bars, following the format: Callback URL|X-VOD-TIMESTAMP|PrivateKey|CallbackContent
   // When changing the private key, we recommend supporting both the old and new keys during a transition period to account for propagation delays. This example shows the calculation for a single key only.
   md5Content := fmt.Sprintf("%s|%s|%s|%s", url, timestamp, privateKey, callbackContent)
   // Calculate the MD5 hash of the concatenated content
   hash := md5.New()
   hash.Write([]byte(md5Content))
   sign := hex.EncodeToString(hash.Sum(nil))
   // Check if it matches the X-VOD-SIGNATURE header
   if sign == r.Header.Get("X-VOD-SIGNATURE") {
      // Authentication success
   } else {
      // Authentication failure
   }
}
```



</Tab>
<Tab zoneid="xgnoFQsoL7" title="Python">
<TabTitle>Python</TabTitle>

Python demo:

```Python
import hashlib
import base64

def callback():
    url = request.url
    content = str(base64.b64encode(request.data), 'utf-8')
    # The header is case-insensitive, so we need to use 'get' to retrieve it
    timestamp = request.headers.get('X-VOD-TIMESTAMP')
    # Verify if X-VOD-TIMESTAMP is within a certain time range
    # todo
    # Signature verification rule: concatenate using vertical bars, following the format: Callback URL|X-VOD-TIMESTAMP|PrivateKey|CallbackContent
    # When modifying the private key, it is recommended to configure both keys for a certain period of time, as there may be a delay in the configuration taking effect. Only one key calculation result is provided here.
    private_key = 'privateKey'
    signature = hashlib.md5("{}|{}|{}|{}".format(url, timestamp, private_key, content).encode("utf-8")).hexdigest()
    if signature == request.headers.get('X-VOD-SIGNATURE'):
        # Authentication passed
    else:
        # Authentication failed
    json_data = {"code": 0, "message": "success"}
    return jsonify(json_data)
```



</Tab>
<Tab zoneid="Fx56HetP8w" title="Java">
<TabTitle>Java</TabTitle>

Java demo:

```Java
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.util.Base64;

public class MyCallbackHandler {

    public String callback(HttpServletRequest request, HttpServletResponse response) {
        String url = request.getRequestURL().toString();
        String content = new String(Base64.getEncoder().encode(getRequestBody(request)), StandardCharsets.UTF_8);
        // The header is case-insensitive, so we need to use 'getHeader' to retrieve it
        String timestamp = request.getHeader("X-VOD-TIMESTAMP");

        // Verify if X-VOD-TIMESTAMP is within a certain time range
        // todo

        // Signature verification rule: concatenate using vertical bars, following the format: Callback URL|X-VOD-TIMESTAMP|PrivateKey|CallbackContent
        // When changing the private key, we recommend supporting both the old and new keys during a transition period to account for propagation delays. This example shows the calculation for a single key only.
        String privateKey = "privateKey";
        String signature = calculateSignature(url, timestamp, privateKey, content);

        if (signature.equals(request.getHeader("X-VOD-SIGNATURE"))) {
            // Authentication passed
        } else {
            // Authentication failed
        }

        String jsonResponse = "{\"code\": 0, \"message\": \"success\"}";
        return jsonResponse;
    }

    private byte[] getRequestBody(HttpServletRequest request) {
        // Get the request body content and convert it to a byte array
        try (InputStream inputStream = request.getInputStream();
             ByteArrayOutputStream outputStream = new ByteArrayOutputStream()) {
            byte[] buffer = new byte[4096];
            int bytesRead;
            while ((bytesRead = inputStream.read(buffer)) != -1) {
                outputStream.write(buffer, 0, bytesRead);
            }
            return outputStream.toByteArray();
        } catch (IOException e) {
            e.printStackTrace();
            return new byte[0];
        }
    }

    private String calculateSignature(String url, String timestamp, String privateKey, String content) {
        String message = url + "|" + timestamp + "|" + privateKey + "|" + content;
        try {
            MessageDigest md = MessageDigest.getInstance("MD5");
            byte[] digest = md.digest(message.getBytes(StandardCharsets.UTF_8));
            StringBuilder sb = new StringBuilder();
            for (byte b : digest) {
                sb.append(String.format("%02x", b));
            }
            return sb.toString();
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
            return null;
        }
    }

}
```



</Tab>
<Tab zoneid="UU9e4hdI8y" title="PHP">
<TabTitle>PHP</TabTitle>

PHP demo:

```PHP
<?php

function callback() {
    $protocol = isset($_SERVER['HTTPS']) && $_SERVER['HTTPS'] == 'on' ? 'https://' : 'http://';
    $url = $protocol . $_SERVER['HTTP_HOST'] . $_SERVER['REQUEST_URI'];
    $content = base64_encode(file_get_contents('php://input'));
    // The header is case-insensitive, so we need to use 'get' to retrieve it
    $timestamp = $_SERVER['HTTP_X_VOD_TIMESTAMP'];
  
    // Verify if X-VOD-TIMESTAMP is within a certain time range
    // todo
  
    // Signature verification rule: concatenate using vertical bars, following the format: Callback URL|X-VOD-TIMESTAMP|PrivateKey|CallbackContent
    // When changing the private key, we recommend supporting both the old and new keys during a transition period to account for propagation delays. This example shows the calculation for a single key only.
    $private_key = 'privateKey';
    $signature = md5($url . '|' . $timestamp . '|' . $private_key . '|' . $content);
  
    if ($signature == $_SERVER['HTTP_X_VOD_SIGNATURE']) {
        // Authentication passed
    } else {
        // Authentication failed
    }
  
    $json_data = array("code" => 0, "message" => "success");
    return json_encode($json_data);
}

?>
```



</Tab>
</Tabs>


<span id="310bc9e8"></span>
## Changing the authentication key

When changing the authentication key, your receiving server needs to be compatible with both the old and new keys for a period of time to prevent callback authentication issues.

The following process is provided for reference:


1. Define a new authentication key.

2. Upgrade the receiving server to support both the old and new authentication keys.

3. Update the authentication key in the BytePlus VOD console to the new key.

4. Wait a period of time, and then remove compatibility with the original authentication key from the receiving server.
