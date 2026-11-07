---
title: "Authentication"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/132442"
---

WTN provides flexible authentication strategies for both pushing and pulling streams. Based on your application's security requirements, you can choose between two methods: no authentication or token\-based authentication.


* **No Authentication (Default):**  WTN allows API calls without authentication by default. This method is suitable for quick integration and testing, or for scenarios with restrictions on URL length.

* **Token\-based Authentication**: Authentication for push and pull streams can be configured independently. To safeguard your business data and prevent unauthorized access and publishing, we strongly recommend enabling token\-based authentication in production environments where secure content delivery is required.


<span id="authentication-process"></span>
## Authentication Process

The full authentication process is as follows.

> You must implement the code logic for steps 1, 2, 3, and 4.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5b7626fdcd7e03abf47350aaa192bfdb.png) </span>

<span id="generate-token"></span>
## Generate Token

<span id="implementation"></span>
### Implementation


1. Enable push/pull stream authentication.

   1. Access the [Console_Feature Configuration](https://console.byteplus.com/rtc/cloudRTC?tab=pushPullStreamAuth), and select your target application.

   2. In the **Push/Pull stream authentication** tab, enable the toggle for "Push stream authentication" or "Pull stream authentication" based on your needs.

      * **Push stream authentication**: When enabled, only clients with a valid token can successfully publish audio/video streams.

      * **Pull stream authentication**: When enabled, only clients with a valid token can subscribe to audio/video streams. This is suitable for scenarios requiring access control, such as paid content or private meetings.

         <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_29aac7c7e439854b0cd88bfe80caad46.png) </span>

2. Generate the token on your server.

   Refer to the generation [Algorithm](https://docs.byteplus.com/docs/byteplus-rtc/132442#algorithm) and [sample code](https://docs.byteplus.com/docs/byteplus-rtc/132442#samplecode) below to generate a token on your application server.


<span id="algorithm"></span>
### Algorithm

Algorithm: Use [JSON Web Tokens](https://jwt.io/) with HS256:

```Plain
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
   YourAppKey
)
```


Parameters:


* Header: Fixed value.


```Plain
{
  "alg": "HS256",
  "typ": "JWT"
}
```



* payload:

   
   |Field |Type |Required |Description |
   |---|---|---|---|
   |version |String |Yes |The version number. Must be set to "1.0". |
   |appID |String |Yes |Your RTC AppID, which can be obtained from the console. |
   |exp |Number |Yes |The expiration timestamp in Unix time (seconds). The token will become invalid after this time. A new token must be generated to republish a stream after expiration. |
   |action |String |Yes |The operation permitted by this token. Valid values are:<br><br><br>* pub: Publish a stream only.<br><br>* sub: Subscribe to a stream only.<br><br>* pub\-sub: Both publish and subscribe on the same connection. |
   |streamID |String |Yes |A unique identifier for the media stream, which you must define. It supports only numbers, letters, and underscores, with a maximum length of 64 characters.<br><br><br>* If action is pub\-sub, two stream IDs must be provided, separated by a forward slash (/), for example: {PubStreamID}/{SubStreamID}.<br><br>* If action is pub or sub, a single StreamID is required. |
   


<span id="sample-code"></span>
### Sample Code  

Use the following sample code to implement token generation on your application server.

Here is a sample in Go:

```go
import (
   "github.com/golang-jwt/jwt/v4"
   "time"
)

func main() {
    appKey := []byte("aaa")
    claims := jwt.NewWithClaims(jwt.SigningMethodHS256, jwt.MapClaims{
       "version":        "1.0",
       "appID":          "2xxxxx",
       "exp":            time.Now().Unix() + 111,
       "action":         "pub", // "pub" allows publishing a stream; "sub" allows subscribing to a stream
       "streamID":       "111",
    })
    
    token, err := claims.SignedString(appKey)
}
```
