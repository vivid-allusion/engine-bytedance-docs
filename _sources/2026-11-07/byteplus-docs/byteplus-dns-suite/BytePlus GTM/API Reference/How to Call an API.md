---
title: "How to Call an API"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/FvV-sD"
---

You invoke the BytePlus Global Traffic Management (GTM) API through an HTTP request.

Before sending an HTTP request, you need to understand the following:


* [Request structure](https://docs.byteplus.com/en/docs/36/20118#request-structure).

* [Common parameters](https://docs.byteplus.com/en/docs/36/20118#common-parameters).

* [Request authentication](https://docs.byteplus.com/en/docs/36/20118#includedinreqheader).


<span id="request-structure"></span>
## Request structure

The structure of an API request contains the following:


* API domain.

* Communication protocol.

* Request method.

* Request parameters.


<span id="api-domain"></span>
### API domain

The API domain for BytePlus GTM is `gtm.byteplusapi.com`.

<span id="communication-protocol"></span>
### Communication protocol

Only the `HTTPS` protocol is supported for API requests. All requests must be sent over HTTPS to ensure secure communication.

<span id="request-method"></span>
### Request method

Please refer to the description of each API for the request method used. For POST requests, you must specify `Content-Type: application/json` in the request header.

<span id="request-parameters"></span>
### Request parameters

Request parameters include common parameters and those specific to each API.

<span id="common-parameters"></span>
## Common parameters

Common parameters are required for every API request. If an API request is missing common parameters, the request will fail. The following table lists the common parameters that must be included in the query string.


|Parameter Name |Data Type |Required |Description |Example |
|---|---|---|---|---|
|Action |string |Yes |Indicates the API name. The format must comply with `[a-zA-Z]+`. |`StartRouting` |
|Version |string |Yes |Indicates the API version. The value of this parameter is `2023-01-01`. |`2023-01-01` |
|X\-Expires |Integer |No |The effective duration of the signature, measured in seconds. The default value is 900. |`900` |


<span id="sample-code-for-request-authentication"></span>
## Sample code for request authentication

Each request must include authentication information. This information is used to verify the identity of the requester.

<span id="golang-sample-code"></span>
### Golang sample code

The following example code demonstrates how to implement request authentication in Golang, and it uses the generated signature to call the GetGtm API and UpdateGtm API.

Before you run the example code, you need to [get your Access Key ID and Secret Access Key](https://console.byteplus.com/iam/keymanage). Then, you will need to pass the values of the Access Key ID and Secret Access Key into the `AccessKey` and `SecretAccessKey` constants in the example code respectively.

```golang
package main

import (
    "bytes"
    "crypto/hmac"
    "crypto/sha256"
    "encoding/hex"
    "encoding/json" 
    "fmt"
    "io/ioutil"
    "net/http"
    "net/url"
    "strings"
    "time"
)

const Version = "2023-01-01"
const Service = "gtm"
const Region = "ap-southeast-1"
const Host = "gtm.byteplusapi.com"

func hmacSHA256(key []byte, content string) []byte {
    mac := hmac.New(sha256.New, key)
    mac.Write([]byte(content))
    return mac.Sum(nil)
}

func hashSHA256(content []byte) string {
    h := sha256.New()
    h.Write(content)
    return hex.EncodeToString(h.Sum(nil))
}

type RequestParam struct {
    Body        []byte
    Method    string
    Date        time.Time
    Path        string
    Host        string
    QueryList url.Values
}

type Credentials struct {
    AccessKeyID     string
    SecretAccessKey string
    Service           string
    Region            string
}

type SignRequest struct {
    XDate            string
    Host             string
    ContentType    string
    XContentSha256 string
    Authorization  string
}

// go http client
var httpClient = &http.Client{
    Timeout: time.Second * 60,
    Transport: &http.Transport{
        MaxIdleConns:    100,
        MaxConnsPerHost: 10,
        IdleConnTimeout: time.Second * 15,
    },
}

func requestGTM(method string, query map[string][]string, header map[string]string, ak string, sk string, action string, body []byte) ([]byte, error) {

    request, _ := http.NewRequest(method, "https://"+Host+"/", bytes.NewReader(body))
    urlVales := url.Values{}
    for k, v := range query {
        urlVales[k] = v
    }
    urlVales["Action"] = []string{action}
    urlVales["Version"] = []string{Version}
    request.URL.RawQuery = urlVales.Encode()
    for k, v := range header {
        request.Header.Set(k, v)
    }

    credential := Credentials{
        AccessKeyID:     ak,
        SecretAccessKey: sk,
        Service:           Service,
        Region:            Region,
    }

    requestParam := RequestParam{
        Body:        body,
        Host:        request.Host,
        Path:        "/",
        Method:    request.Method,
        Date:        time.Now().UTC(),
        QueryList: request.URL.Query(),
    }

    xDate := requestParam.Date.Format("20060102T150405Z")
    shortXDate := xDate[:8]
    XContentSha256 := hashSHA256(requestParam.Body)
    contentType := "application/json"
    signResult := SignRequest{
        Host:             requestParam.Host, 
        XContentSha256: XContentSha256,    
        XDate:            xDate,              
        ContentType:    contentType,         
    }

    signedHeadersStr := strings.Join([]string{"content-type", "host", "x-content-sha256", "x-date"}, ";")
    canonicalRequestStr := strings.Join([]string{
        requestParam.Method,
        requestParam.Path,
        request.URL.RawQuery,
        strings.Join([]string{"content-type:" + contentType, "host:" + requestParam.Host, "x-content-sha256:" + XContentSha256, "x-date:" + xDate}, "\n"),
        "",
        signedHeadersStr,
        XContentSha256,
    }, "\n")
    hashedCanonicalRequest := hashSHA256([]byte(canonicalRequestStr))
    credentialScope := strings.Join([]string{shortXDate, credential.Region, credential.Service, "request"}, "/")
    stringToSign := strings.Join([]string{
        "HMAC-SHA256",
        xDate,
        credentialScope,
        hashedCanonicalRequest,
    }, "\n")
    kDate := hmacSHA256([]byte(credential.SecretAccessKey), shortXDate)
    kRegion := hmacSHA256(kDate, credential.Region)
    kService := hmacSHA256(kRegion, credential.Service)
    kSigning := hmacSHA256(kService, "request")
    signature := hex.EncodeToString(hmacSHA256(kSigning, stringToSign))
    signResult.Authorization = fmt.Sprintf("HMAC-SHA256 Credential=%s, SignedHeaders=%s, Signature=%s", credential.AccessKeyID+"/"+credentialScope, signedHeadersStr, signature)

    request.Header.Set("Host", signResult.Host)
    request.Header.Set("Content-Type", signResult.ContentType)
    request.Header.Set("X-Date", signResult.XDate)
    request.Header.Set("X-Content-Sha256", signResult.XContentSha256)
    request.Header.Set("Authorization", signResult.Authorization)
    resp, err := httpClient.Do(request)
    if err != nil {
        return nil, err
    }
    body, err = ioutil.ReadAll(resp.Body)
    if err != nil {
        return nil, err
    }
    return body, nil
}

/* main.go */

type UpdateGtmParam struct {
    GtmId  string `json:"GtmId"`
    Remark string `json:"Remark"`
}

func main() {
    // Call UpdateGtm API
    bodyParam := UpdateGtmParam{
        GtmId:  "27db6621-a70d-4cac-bba5-**********",
        Remark: "example",
    }
    body, err := json.Marshal(&bodyParam)
    if err != nil {
        fmt.Printf("marshal failed: %v", err)
        return
    }
 
    AccessKey := "Access Key ID"
    SecretAccessKey := "Secret Access Key"
 
    updateGtmResult, err := requestGTM("POST", map[string][]string{}, map[string]string{}, AccessKey, SecretAccessKey, "UpdateGtm", body)
    if err != nil {
        fmt.Printf("do request failed: %v", err)
        return
    }
    fmt.Println(string(updateGtmResult))
 
    // Call GetGtm API
    QueryParam := map[string][]string{"GtmId": []string{"27db6621-a70d-4cac-bba5-********"}}
 
    getGtmResult, err := requestGTM("POST", QueryParam, map[string]string{}, AccessKey, SecretAccessKey,
        "GetGtm", []byte{})
    if err != nil {
        fmt.Printf("do request failed: %v", err)
        return
    }
    fmt.Println(string(getGtmResult))
 
}
```


<span id="python-3-sample-code"></span>
### Python 3 sample code

The following sample code demonstrates how to implement the signing mechanism in Python 3, and it uses the generated signature to call the ListGtms API.

Before running the sample code, you need to [get your Access Key ID and Secret Access Key](https://console.byteplus.com/iam/keymanage). Then, you will need to insert the values of the Access Key ID and Secret Access Key into the `AK` and `SK` variables in the sample code, respectively. Additionally, the sample code uses the [requests](https://pypi.org/project/requests/) library, which you can install with the command `python3 -m pip install requests`.

```python
# Python3
import datetime
import hashlib
import hmac
import json
from urllib.parse import quote
from collections import OrderedDict

import requests

Service = "gtm"
Version = "2023-01-01"
Region = "ap-southeast-1"
Host = "gtm.byteplusapi.com"

AK = "AK"
SK = "SK"


def norm_query(params):
    query = ""
    for key in sorted(params.keys()):
        if type(params[key]) == list:
            for k in params[key]:
                query = (
                        query + quote(key, safe="-_.~") + "=" + quote(k, safe="-_.~") + "&"
                )
        else:
            query = (query + quote(key, safe="-_.~") + "=" + quote(params[key], safe="-_.~") + "&")
    query = query[:-1]
    return query.replace("+", "%20")

def hmac_sha256(key: bytes, content: str):
    return hmac.new(key, content.encode("utf-8"), hashlib.sha256).digest()


def hash_sha256(content: str):
    return hashlib.sha256(content.encode("utf-8")).hexdigest()


def request(method, query, header, ak, sk, action, body):

    credential = {
        "access_key_id": ak,
        "secret_access_key": sk,
        "service": Service,
        "region": Region,
    }

    query = {"Action": action, "Version": Version, **query}
    sorted_query = OrderedDict(sorted(query.items()))

    request_param = {
        "body":json.dumps(body),
        "host": Host,
        "path": "/",
        "method": method,
        "content_type": "application/json",
        "date": datetime.datetime.utcnow(),
        "query": sorted_query,
    }


    x_date = request_param["date"].strftime("%Y%m%dT%H%M%SZ")
    short_x_date = x_date[:8]
    x_content_sha256 = hash_sha256(request_param["body"])
    sign_result = {
        "Host": request_param["host"],
        "X-Content-Sha256": x_content_sha256,
        "X-Date": x_date,
        "Content-Type": request_param["content_type"],
    }

    signed_headers_str = ";".join(
        ["content-type", "host", "x-content-sha256", "x-date"]
    )
    canonical_request_str = "\n".join(
        [request_param["method"],
         request_param["path"],
         norm_query(request_param["query"]),
         "\n".join(
             [
                 "content-type:" + request_param["content_type"],
                 "host:" + request_param["host"],
                 "x-content-sha256:" + x_content_sha256,
                 "x-date:" + x_date,
             ]
         ),
         "",
         signed_headers_str,
         x_content_sha256,
         ]
    )
    hashed_canonical_request = hash_sha256(canonical_request_str)
    credential_scope = "/".join([short_x_date, credential["region"], credential["service"], "request"])
    string_to_sign = "\n".join(["HMAC-SHA256", x_date, credential_scope, hashed_canonical_request])
    k_date = hmac_sha256(credential["secret_access_key"].encode("utf-8"), short_x_date)
    k_region = hmac_sha256(k_date, credential["region"])
    k_service = hmac_sha256(k_region, credential["service"])
    k_signing = hmac_sha256(k_service, "request")
    signature = hmac_sha256(k_signing, string_to_sign).hex()
    sign_result["Authorization"] = "HMAC-SHA256 Credential={}, SignedHeaders={}, Signature={}".format(
        credential["access_key_id"] + "/" + credential_scope,
        signed_headers_str,
        signature,
    )
    header = {**header, **sign_result}

    r = requests.post("https://{}{}".format(request_param["host"], request_param["path"]),
                        headers=header,
                        params=request_param["query"],
                        data=request_param["body"],
                        )
    return r.json()


if __name__ == "__main__":
    # Call UpdateGtm API
    request_body = {
        "GtmId": "27db6621-a70d-4cac-bba5-**********",
        "Remark": "example",
    }
    update_gtm_result = request("POST", {}, {}, AK, SK, "UpdateGtm", request_body)
    print(update_gtm_result)

    # Call GetGtm API
    request_query = {"GtmId": "27db6621-a70d-4cac-bba5-**********"}
    get_gtm_result = request("POST", request_query, {}, AK, SK, "GetGtm", {})
    print(get_gtm_result)
```
