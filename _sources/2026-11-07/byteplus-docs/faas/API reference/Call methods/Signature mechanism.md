---
title: "Signature mechanism"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Signature_mechanism"
---

For each access request, the BytePlus verifies the identity of the access requestor through the access key (including Access Key ID and Secret Access Key) in the access signature information.

<span id="获取访问密钥"></span>
## Obtain access key

Accounts and users with permission can create access keys in the following operation:


1. Use the root user or an IAM user with key management permissions to log in to the [Identity and Access Management console](https://console.byteplus.com/iam).

2. In the left navigation bar select **Resource Management \> Key Management**.

3. View the list of access keys for your account.

   * Each account has a maximum of two access keys simultaneously.

   * If the current account does not have the maximum number of access keys, click **Create Access Key** to create a new access key. After creating, click **View Access Key details** to view the information of the new access key.


<span id="创建一个正规化请求"></span>
## Create a normalization request

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Hash refers to the SHA256 algorithm.</div>


* <div data-tips="true" data-tips-type="tip">HexEncode refers to changing to hexadecimal encoding.</div>



```Plain Text
CanonicalRequest = HTTPRequestMethod + '\n' + CanonicalURI + '\n' + CanonicalQueryString + '\n' + CanonicalHeaders + '\n' + SignedHeaders + '\n' + HexEncode(Hash(RequestPayload))
```


Before signing, the request should be normalized so that the signature calculation process has no objections. The main process and pseudocode are as follows:


|Field |Description |
|---|---|
|HTTPRequestMethod |HTTP request method, e.g. POST. |
|CanonicalURI |The normalized URI. If the URI is empty, then use`/`as an absolute path. |
|CanonicalQueryString |Normalized QueryString. The QueryString normalization process is as follows:<br><br><br>1. URL Encode the parameter name and parameter value of each QueryString.<br><br>2. Strict ordering of parameter names in ASCII byte order.<br><br>3. Connect the parameter names and parameter values in the sorted order using`=`Connect the parameter pairs according to sorted results using`&`Connect.<br><br><br>```Plain Text```<br>```CanonicalQueryString = "Action=ListUsers&Version=2018-01-01"```<br> |
|CanonicalHeaders |Header after normalization. The pseudocode is as follows:<br><br>```Plain Text```<br>```CanonicalHeaders = CanonicalHeadersEntry0 + CanonicalHeadersEntry1 + ... + CanonicalHeadersEntryN```<br><br><br>```Plain Text```<br>```CanonicalHeadersEntry = Lowercase(HeaderName) + ':' + Trimall(HeaderValue) + '\n'```<br><br><br>Among them, `Lowercase` means to convert all the names of the Header to lowercase, and `Trimall` means to remove the excess spaces before and after the value of the Header.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You need to add line\-changing characters: '\n' at the end.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The order of the Header is ASCII sorted by the lowercase of the <code>headerName</code>.</div><br> |
|SignedHeaders |The name of the Header participating in the signature. The signature Header should be included in the list of normalized Headers to indicate which Headers participate in the signature calculation, thus ignoring the additional Headers added by the proxy. If there are two Headers `host` and `x-date`, then they must be added to the list of normalized Header names. <br><br>The pseudocode is as follows:<br><br>```Plain Text```<br>```SignedHeaders = Lowercase(HeaderName0) + ';' + Lowercase(HeaderName1) + ";" + ... + Lowercase(HeaderNameN)```<br> |
|RequestPayload |Complete request body.<br><br><br>* The URL encodes the parameter name and parameter value of each QueryString (the same as the [RFC3986](https://tools.ietf.org/html/rfc3986) method).<br><br>   Here, the GET method needs to include all parameters of hash algorithm, trust certificate, signature date, and signature Header, etc.<br><br>* Strict ordering of parameter names in ASCII byte order.<br><br>* Connect the parameter names and parameter values in the sorted order using`=`Connect the parameter pairs according to sorted results using`&`Connect. |


<span id="创建签名字符串"></span>
## Create signature string

The signature string mainly contains the metadata information of the request and the normalization request. It consists of the signature algorithm, the request date, the trust certificate, and the normalization request hash value connection. The pseudocode is as follows:

```Plain Text
StringToSign = Algorithm + '\n' + RequestDate + '\n' + CredentialScope + '\n' + HexEncode(Hash(CanonicalRequest))
```


The field description is as follows.


|Field |Description |
|---|---|
|Algorithm |The algorithm for signature. The current BytePlus only supports the HMAC\-SHA256 signature algorithm. |
|RequestDate |Request UTC time. Please use `YYYYMMDD T'HHMMSS'Z'`format, e.g.: `20201103T104027Z`. |
|CredentialScope |Scope of credentials. The format is `YYYYMMDD/region/service/request`. |
|CanonicalRequest |The result of a preorder normalization request. |


<span id="计算签名秘钥"></span>
## Calculate signature key


1. Before calculating the signature, first derive the Signing Key from the Secret Access Key, rather than directly using the Secret Access Key. The specific calculation process is as follows:

   ```Plain Text
   kSecret = *Your Secret Access Key*
   kDate = HMAC(kSecret, Date)
   kRegion = HMAC(kDate, Region)
   kService = HMAC(kRegion, Service)
   kSigning = HMAC(kService, "request")
   ```
   

2. Calculate the signature.

   ```Plain Text
   Signature = HexEncode(HMAC(kSigning, StringToSign))
   ```
   

3. Build the Header.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Use in the expression<code>{}</code>the content, representing the middle process calculated in the above.   </div>
   

   ```Plain Text
   Authorization: HMAC-SHA256 Credential={AccessKeyId}/{CredentialScope}, SignedHeaders={SignedHeaders}, Signature={Signature}
   ```
   


<span id="代码示例"></span>
## Sample code

The following is the Golang implementation of the signature mechanism. After signing, the FaaS OpenAPI ListFunctions interface is called.

```Bash
package main

import (
    "bytes"
    "crypto/hmac"
    "crypto/sha256"
    "encoding/hex"
    "fmt"
    "log"
    "net/http"
    "net/http/httputil"
    "net/url"
    "strings"
    "time"
)

const (
    AccessKeyID     = "AKxxx"
    SecretAccessKey = "yyyyyy"

    Addr = "https://iam.byteplusapi.com"
    Path = "/" // path without Query

    Service = "vefaas"
    Region  = "ap-southeast-1"
    Action  = "ListFunctions"
    Version = "2024-06-06"
)

func hmacSHA256(key []byte, content string) []byte {
    mac := hmac.New(sha256.New, key)
    mac.Write([]byte(content))
    return mac.Sum(nil)
}

func getSignedKey(secretKey, date, region, service string) []byte {
    kDate := hmacSHA256([]byte(secretKey), date)
    kRegion := hmacSHA256(kDate, region)
    kService := hmacSHA256(kRegion, service)
    kSigning := hmacSHA256(kService, "request")

    return kSigning
}

func hashSHA256(data []byte) []byte {
    hash := sha256.New()
    if _, err := hash.Write(data); err != nil {
       log.Printf("input hash err:%s", err.Error())
    }

    return hash.Sum(nil)
}

func doRequest(method string, queries url.Values, body []byte) error {
    // 1. Build request
    queries.Set("Action", Action)
    queries.Set("Version", Version)
    requestAddr := fmt.Sprintf("%s%s?%s", Addr, Path, queries.Encode())
    log.Printf("request addr: %s\n", requestAddr)

    request, err := http.NewRequest(method, requestAddr, bytes.NewBuffer(body))
    if err != nil {
       return fmt.Errorf("bad request: %w", err)
    }

    // 2. Build the signature material
    now := time.Now()
    date := now.UTC().Format("20060102T150405Z")
    authDate := date[:8]
    request.Header.Set("X-Date", date)

    payload := hex.EncodeToString(hashSHA256(body))
    request.Header.Set("X-Content-Sha256", payload)
    request.Header.Set("Content-Type", "application/x-www-form-urlencoded")

    queryString := strings.Replace(queries.Encode(), "+", "%20", -1)
    signedHeaders := []string{"host", "x-date", "x-content-sha256", "content-type"}
    var headerList []string
    for _, header := range signedHeaders {
       if header == "host" {
          headerList = append(headerList, header+":"+request.Host)
       } else {
          v := request.Header.Get(header)
          headerList = append(headerList, header+":"+strings.TrimSpace(v))
       }
    }
    headerString := strings.Join(headerList, "\n")

    canonicalString := strings.Join([]string{
       method,
       Path,
       queryString,
       headerString + "\n",
       strings.Join(signedHeaders, ";"),
       payload,
    }, "\n")
    log.Printf("canonical string:\n%s\n", canonicalString)

    hashedCanonicalString := hex.EncodeToString(hashSHA256([]byte(canonicalString)))
    log.Printf("hashed canonical string: %s\n", hashedCanonicalString)

    credentialScope := authDate + "/" + Region + "/" + Service + "/request"
    signString := strings.Join([]string{
       "HMAC-SHA256",
       date,
       credentialScope,
       hashedCanonicalString,
    }, "\n")
    log.Printf("sign string:\n%s\n", signString)

    // 3. Build the authentication request header
    signedKey := getSignedKey(SecretAccessKey, authDate, Region, Service)
    signature := hex.EncodeToString(hmacSHA256(signedKey, signString))
    log.Printf("signature: %s\n", signature)

    authorization := "HMAC-SHA256" +
       " Credential=" + AccessKeyID + "/" + credentialScope +
       ", SignedHeaders=" + strings.Join(signedHeaders, ";") +
       ", Signature=" + signature
    request.Header.Set("Authorization", authorization)
    log.Printf("authorization: %s\n", authorization)

    // 4. Print the request and initiate the request
    requestRaw, err := httputil.DumpRequest(request, true)
    if err != nil {
       return fmt.Errorf("dump request err: %w", err)
    }

    log.Printf("request:\n%s\n", string(requestRaw))

    response, err := http.DefaultClient.Do(request)
    if err != nil {
       return fmt.Errorf("do request err: %w", err)
    }

    // 5. Print response
    responseRaw, err := httputil.DumpResponse(response, true)
    if err != nil {
       return fmt.Errorf("dump response err: %w", err)
    }

    log.Printf("response:\n%s\n", string(responseRaw))

    if response.StatusCode == 200 {
       log.Printf("Request successful")
    } else {
       log.Printf("Request failed")
    }

    return nil
}

func main() {
    // GET request example
    query1 := make(url.Values)
    doRequest(http.MethodGet, query1, nil)

}
```


&nbsp;
