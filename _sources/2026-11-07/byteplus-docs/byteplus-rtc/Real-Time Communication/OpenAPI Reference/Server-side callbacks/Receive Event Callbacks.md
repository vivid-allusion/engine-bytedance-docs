---
title: "Receive Event Callbacks"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69820"
---

<span id="introduction"></span>
## Introduction

To receive callbacks from the RTC server, you must deploy an HTTP (s) service on your business server. The RTC server sends a POST request to the URL that you specify on your business server. The URL receives event detail callbacks from the RTC server. The following table lists conditions for receiving callbacks.


|Condition |Callback |Solution |
|---|---|---|
|HTTP status code:`200` |Succeed | |
|* HTTP status code: `!=200`<br><br>* The response time exceeds 5s |Fail |The RTC server will retry up to 2 times (no more than 3 callbacks in total). |


Currently, the uniqueness of callback events cannot be guaranteed. It is recommended that you use the [EventId](https://docs.byteplus.com/en/docs/12/docs-75124#callback-parameters) to deduplicate callback events.

RTC will sign the server\-side callback. If you wish to verify that the source is indeed BytePlus RTC and that the content has not been tampered with, you can check the callback signature; otherwise, you may ignore the callback signature. If you need to verify the signature, please refer to the following algorithm and implementation.

<span id="signature-algorithm"></span>
## Signature algorithm

When RTC server initiates a callback, it uses the callback secretkey you set to sign the callback. You can refer to the signature algorithm below for signature verification:


1. Combine the secret key with the event parameters to form an array.


```Go
type Event struct {
        EventType string `json:"EventType"`
        EventData string `json:"EventData"`
EventTime string json: asset EventTime output
        EventId   string `json:"EventId"`
        AppId     string `json:"AppId"`
        Version   string `json:"Version"`
        Nonce      string `json:"Nonce"`
        Signature string `json:"Signature"`
}
var event Event
data := []string{
        event.EventType,
        event.EventData,
event. EventTime,
        event.EventId,
        event.AppId,
        event.Version,
        event.Nonce,
        secretKey,
}
```


> Example : [EventTypeVal EventDataVal EventTimeVal EventIdVal VersionVal AppIDVal NonceVal SecretKeyVal]


2. Alphabetically sort the values in the array.


```Plain Text
SortedData = Sort(data)
```


> Example : [AppIDVal EventDataVal EventIdVal EventTimeVal EventTypeVal NonceVal SecretKeyVal VersionVal]


3. Join the sorted values into a string to get PayloadData.


```Plain Text
PayloadData=Join(SortedData)
```


> Example: '[AppIDValEventDataValEventIdValEventTimeValEventTypeValNonceValSecretKeyValVersionVal]'


5. Apply a hash algorithm to PayloadData.


```Plain Text
HashData=Hash(PayloadData)
```


> Example: [20 170 104 20 32 203 70 171 95 29 138 214 172 154 178 31 52 30 169 219 249 213 35 112 89 195 196 192 231 49 48 15]


6. Encode the resulting hash in hexadecimal format to generate the callback signature.


```Plain Text
Signature=HexEncode(HashData)
```


> Example: 14a681420cb46ab5f1d8ad6ac9ab21f341ea9dbf9d5237059c3c4c0e731300f


<span id="sample-code"></span>
## Sample code

RTC provides sample code in Golang and Java. You can refer to the following sample code for signature verification.

<span id="golang"></span>
### Golang

```Go
import (
   "crypto/sha256"
   "fmt"
   "sort"
   "strings"
)

func main() {
    event := &Event{
        EventType: "RoomCreate",
        EventData: "{\"RoomId\":\"room1\",\"Timestamp\":1679383924691}",
        EventTime: "2023-03-21T15:32:04+08:00",
        EventId:   "123456",
        Version:   "2020-12-01",
        AppId:     "appId",
        Nonce:      "aaBc",
        Signature: "1c7200723842eff514b65fc3f065597432bbb4249e10d33db79b3853d05f3691",
    }
   
    secretKey := "1234"
    ok := CheckSignature(event, secretKey)
    fmt.Printf("the result is %t", ok)
}

type Event struct {
    EventType string `json:"EventType"`
    EventData string `json:"EventData"`
    EventTime string `json:"EventTime"`
    EventId   string `json:"EventId"`
    AppId     string `json:"AppId"`
    Version   string `json:"Version"`
    Signature string `json:"Signature"`
    Nonce      string `json:"Nonce"`
}

func CheckSignature(event *Event, secretKey string) bool {
    data := []string{
        event.EventType,
        event.EventData,
        event.EventTime,
        event.EventId,
        event.AppId,
        event.Version,
        event.Nonce,
        secretKey,
    }
    sort.Strings(data)
    payload := strings.Join(data, "")
    hashData := sha256.Sum256([]byte(payload))
    signature := fmt.Sprintf("%x", hashData)
    fmt.Println("sign:" + signature)
    return signature == event.Signature
}
```


<span id="java"></span>
### Java

```Java
import java.math.BigInteger;
import java.security.MessageDigest;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.security.NoSuchAlgorithmException;

class Event{
    public String EventType;
    public String EventData;
    public String EventTime;
    public String EventId;
    public String AppId;
    public String Version;
    public String Nonce;
    public String Signature;
}

public class CheckSignature {
    public static void main(String[] args) {
        Event event=new Event();
        event.EventType="RoomCreate";
        event.EventData="{\"RoomId\":\"room1\",\"Timestamp\":1679383924691}";
        event.EventTime="2023-03-21T15:32:04+08:00";
        event.EventId="123456";
        event.Version="2020-12-01";
        event.AppId="appId";
        event.Nonce="aaBc";
        event.Signature="1c7200723842eff514b65fc3f065597432bbb4249e10d33db79b3853d05f3691";
        String secretKey="1234";

        boolean ret=Check(event,secretKey);
        System.out.println(ret);

    }
    private static boolean Check(Event event,String secretKey){
        try {
            List<String> data = new ArrayList<>();
            data.add(event.EventType);
            data.add(event.EventData);
            data.add(event.EventTime);
            data.add(event.EventId);
            data.add(event.AppId);
            data.add(event.Version);
            data.add(event.Nonce);
            data.add(secretKey);

            Collections.sort(data);

            final String payloadData=String.join("",data);
            MessageDigest digest = MessageDigest.getInstance("SHA-256");
            digest.update(payloadData.getBytes());
            String signature=byteToHexString(digest.digest());
            System.out.println(signature);

            if(event.Signature.equals(signature)){
                return true;
            }
        } catch (NoSuchAlgorithmException e){
            e.printStackTrace();
        }
        return false;
    }

    private static String byteToHexString(byte[] bytes){
        return String.format("%064x", new BigInteger(1,bytes));
    }
}
```
