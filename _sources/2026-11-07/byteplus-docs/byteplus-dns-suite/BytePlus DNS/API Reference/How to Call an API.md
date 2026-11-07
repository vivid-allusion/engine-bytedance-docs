---
title: "How to Call an API"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-calling-an-api-with-http-requests"
---

You call the BytePlus DNS API using an HTTP request.

Before sending an HTTP request, you need to understand the following:


* Request structure.

* Common parameters.

* Request authentication.


<span id="f1194634"></span>
## Request structure

The structure of an API request includes the following:


* API domain.

* Communication protocol.

* Request method.

* Request parameters.


<span id="72999021"></span>
### API domain

The API domain for BytePlus DNS is `dns.byteplusapi.com`.

<span id="46741927"></span>
### Communication protocol

You can use either the `HTTP` or `HTTPS` protocol to send requests. It is recommended to use the `HTTPS` protocol for higher security.

<span id="c3218b43"></span>
### Request method

Refer to the documentation of each API for the method it uses. For POST requests, you must specify `Content-Type: application/json` in the request header.

<span id="d3564510"></span>
### Request parameters

Request parameters include common parameters and parameters specific to each API.

<span id="e3cf2edd"></span>
## Common parameters

Common parameters are required for every API request. If a common parameter is missing in an API request, the request will fail. The following table lists the common parameters that must be included in the query string.


|**Parameter Name** |**Data Type** |**Required** |**Description** |**Example** |
|---|---|---|---|---|
|Action |String |Yes |The name of the API. The format is `[a-zA-Z]+`. |`CreateZone` |
|Version |String |Yes |The version of the API. The value is `2018-08-01`. |`2018-08-01` |
|X\-Expires |Integer |No |The validity period of the signature in seconds. The default value is 900. |`900` |


<span id="82873929"></span>
## Request authentication example code

Authentication information must be included in each request to verify the identity of the requester.

<span id="8b8c1a58"></span>
### Golang example code

The following example code demonstrates how to authenticate your request when calling UpdateZone API and CheckZone API.

Before running the example code, you need to [get your Access Key ID and Secret Access Key](https://console.byteplus.com/iam/keymanage). Then, you need to pass the values of your Access Key ID and Secret Access Key into the `AccessKey` constant and `SecretAccessKey` constant in the example code, respectively.

```Go
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


const Version = "2018-08-01"
const Service = "DNS"
const Region = "singapore"
const Host = "dns.byteplusapi.com"


// Step 1: Prepare helper functions.
// HMAC-SHA256 encryption
func hmacSHA256(key []byte, content string) []byte {
   mac := hmac.New(sha256.New, key)
   mac.Write([]byte(content))
   return mac.Sum(nil)
}


// SHA256 hash algorithm
func hashSHA256(content []byte) string {
   h := sha256.New()
   h.Write(content)
   return hex.EncodeToString(h.Sum(nil))
}


// Step 2: Prepare the necessary struct definitions.
// Request parameters struct for signing
type RequestParam struct {
   Body      []byte
   Method    string
   Date      time.Time
   Path      string
   Host      string
   QueryList url.Values
}


// Credentials struct for authentication
type Credentials struct {
   AccessKeyID     string
   SecretAccessKey string
   Service         string
   Region          string
}


// SignRequest struct for the result of signing
type SignRequest struct {
   XDate          string
   Host           string
   ContentType    string
   XContentSha256 string
   Authorization  string
}


// Go HTTP client
var httpClient = &http.Client{
   Timeout: time.Second * 60,
   Transport: &http.Transport{
      MaxIdleConns:    100,
      MaxConnsPerHost: 10,
      IdleConnTimeout: time.Second * 15,
   },
}


// Step 3: Create a DNS API request function. The signature calculation process is included in this function.
func requestDNS(method string, query map[string][]string, header map[string]string, ak string, sk string, action string, body []byte) ([]byte, error) {
   // Step 4: In the requestDNS function, create an HTTP request instance.
   // Create an HTTP request instance. This instance will be used later.
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
   // Step 5: Create credentials. The Service and Region fields are fixed. ak and sk represent AccessKeyID and SecretAccessKey, respectively. The signature struct is also initialized here. Some properties required for signature calculation are also handled here.
   // Initialize credentials
   credential := Credentials{
      AccessKeyID:     ak,
      SecretAccessKey: sk,
      Service:         Service,
      Region:          Region,
   }
   // Initialize the signature struct
   requestParam := RequestParam{
      Body:      body,
      Host:      request.Host,
      Path:      "/",
      Method:    request.Method,
      Date:      time.Now().UTC(),
      QueryList: request.URL.Query(),
   }
   // Step 6: Start calculating the signature. Before calculating the signature, prepare the signResult variable to receive the result of the signature calculation and set some parameters.
   // Initialize the signature result struct
   xDate := requestParam.Date.Format("20060102T150405Z")
   shortXDate := xDate[:8]
   XContentSha256 := hashSHA256(requestParam.Body)
   contentType := "application/json"
   signResult := SignRequest{
      Host:           requestParam.Host, // Set Host
      XContentSha256: XContentSha256,    // Encrypt body
      XDate:          xDate,             // Set standardized time
      ContentType:    contentType,       // Set Content-Type to application/json
   }
   // Step 7: Calculate the Signature.
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
   // Step 8: Write the Signature into the HTTP Header and send the HTTP request.
   // Set the 5 signed HTTP Headers
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


// Define the request parameter struct
type UpdateZoneParam struct {
   ZID    uint64 `json:"ZID"`
   Remark string `json:"Remark"`
}


func main() {
   // (POST request) Call UpdateZone API
   bodyParam := UpdateZoneParam{
    ZID:    100,
    Remark: "example",
   }
   body, err := json.Marshal(&bodyParam)
   if err != nil {
      fmt.Printf("marshal failed: %v", err)
      return
   }
   // Pass the values of your Access Key ID and Secret Access Key into the AccessKey constant and SecretAccessKey constant
   AccessKey := "ak"
   SecretAccessKey := "sk"
   updateZoneResult, err := requestDNS("POST", map[string][]string{}, map[string]string{}, AccessKey, SecretAccessKey, "UpdateZone", body)
   if err != nil {
      fmt.Printf("do request failed: %v", err)
      return
   }
    // Print the output result
    fmt.Println(string(updateZoneResult))


    // (GET request) Call CheckZone API
    QueryParam := map[string][]string{"ZoneName": []string{"example.com"}}


    checkZoneResult, err := requestDNS("GET", QueryParam, map[string]string{}, AccessKey, SecretAccessKey,
       "CheckZone", []byte{})
    if err != nil {
       fmt.Printf("do request failed: %v", err)
       return
    }
    // Print the output result
    fmt.Println(string(checkZoneResult))


}
```


<span id="d8da7b5f"></span>
### Java example code

The following example code demonstrates how to authenticate your request when calling UpdateZone API and CheckZone API.

Before running the example code, you need to [get your Access Key ID and Secret Access Key](https://console.byteplus.com/iam/keymanage). Then, you need to pass the values of your Access Key ID and Secret Access Key into the `AK` constant and `SK` constant in the example code, respectively.

```Java
import com.alibaba.fastjson.JSON;
import org.apache.commons.codec.binary.Hex;
import org.apache.http.HttpEntity;
import org.apache.http.NameValuePair;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.client.methods.HttpUriRequest;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.entity.ByteArrayEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.message.BasicNameValuePair;
import org.apache.http.util.EntityUtils;


import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.io.IOException;
import java.net.URI;
import java.net.URISyntaxException;
import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.util.*;


public class MainDNS {


    // Step 1: Prepare the necessary class definitions.
    // Request parameter structure class for signing
    public static class RequestParam {
        public final byte[] body;
        public final String method;
        public final Date date;
        public final String path;
        public final String host;
        public final String contentType;
        public final ArrayList<NameValuePair> queryList;


        public RequestParam(byte[] body, String method, Date date, String path, String host, String contentType, ArrayList<NameValuePair> queryList) {
            this.body = body;
            this.method = method;
            this.date = date;
            this.path = path;
            this.host = host;
            this.contentType = contentType;
            this.queryList = queryList;
        }
    }


    public static final String TIME_FORMAT_V4 = "yyyyMMdd'T'HHmmss'Z'";
    private static final TimeZone tz = TimeZone.getTimeZone("UTC");
    // Pass the values of your Access Key ID and Secret Access Key into the AK constant and SK constant
    private static final String AK = "ak";
    private static final String SK = "sk";
    private static final String Service = "DNS";
    private static final String Version = "2018-08-01";
    private static final String Region = "singapore";
    private static final String Host = "dns.byteplusapi.com";


    // Step 2: Prepare auxiliary functions.
    // sha256 asymmetric encryption
    public static byte[] hmacSHA256(byte[] key, String content) {
        try {
            Mac mac = Mac.getInstance("HmacSHA256");
            mac.init(new SecretKeySpec(key, "HmacSHA256"));
            return mac.doFinal(content.getBytes());
        } catch (Exception e) {
            return null;
        }
    }


    // sha256 hash algorithm
    public static String hashSHA256(byte[] content) {
        try {
            MessageDigest md = MessageDigest.getInstance("SHA-256");
            return Hex.encodeHexString(md.digest(content));
        } catch (Exception e) {
            return null;
        }
    }


    private static String getAppointFormatDate(Date date) {
        DateFormat df = new SimpleDateFormat(TIME_FORMAT_V4);
        df.setTimeZone(tz);
        return df.format(date);
    }


    // Step 3: Create an API request function. The signature calculation process is included in this function.
    public static byte[] request(String method, HashMap<String, String> query, HashMap<String, String> header, String ak, String sk, String action, byte[] body) throws URISyntaxException {


        // Step 4: Create identity proof. The Service and Region fields are fixed. ak and sk represent AccessKeyID and SecretAccessKey respectively.
        // Also initialize the signature object. Some properties required for signature calculation are also handled here.
        // Initialize identity proof
        HashMap<String, String> credential = new HashMap() {
            {
                put("accessKeyId", ak);
                put("secretKeyId", sk);
                put("service", Service);
                put("region", Region);
            }
        };
        ArrayList<NameValuePair> nvps = new ArrayList<>();
        for (Map.Entry<String, String> entry : query.entrySet()) {
            nvps.add(new BasicNameValuePair(entry.getKey(), entry.getValue()));
        }
        nvps.add(new BasicNameValuePair("Action", action));
        nvps.add(new BasicNameValuePair("Version", Version));
        Collections.sort(nvps, new Comparator<NameValuePair>() {
            @Override
            public int compare(NameValuePair o1, NameValuePair o2) {
                return o1.getName().compareTo(o2.getName());
            }
        });


        // Initialize signature structure
        RequestParam requestParam = new RequestParam(body, method, new Date(), "/", Host, "application/json", nvps);
        URI uri = new URIBuilder().addParameters(requestParam.queryList).build();
        // Step 5: Start calculating the signature
        // Initialize the signature result variable
        String xDate = getAppointFormatDate(new Date());
        String shortXDate = xDate.substring(0, 8);
        String xContentSha256 = hashSHA256(body);
        // Step 6: Calculate the signature
        String[] headStr = {"content-type", "host", "x-content-sha256", "x-date"};
        String signedHeadersStr = String.join(";", headStr);
        String[] headStrSecond = {"content-type:" + requestParam.contentType, "host:" + requestParam.host, "x-content-sha256:" + xContentSha256, "x-date:" + xDate};
        String preRequestStr = String.join("\n", headStrSecond);
        String[] preCanonicalRequestStr = {requestParam.method, requestParam.path, uri.getRawQuery(), preRequestStr, "", signedHeadersStr, xContentSha256};
        String canonicalRequestStr = String.join("\n", preCanonicalRequestStr);
        String hashedCanonicalRequest = hashSHA256(canonicalRequestStr.getBytes());
        String[] credentialStr = {shortXDate, credential.get("region"), credential.get("service"), "request"};
        String credentialScope = String.join("/", credentialStr);


        String[] preStringToSign = {"HMAC-SHA256", xDate, credentialScope, hashedCanonicalRequest};
        String stringToSign = String.join("\n", preStringToSign);
        byte[] kDate = hmacSHA256(credential.get("secretKeyId").getBytes(), shortXDate);
        byte[] kRegion = hmacSHA256(kDate, credential.get("region"));
        byte[] kService = hmacSHA256(kRegion, credential.get("service"));
        byte[] kSigning = hmacSHA256(kService, "request");
        String signature = Hex.encodeHexString(hmacSHA256(kSigning, stringToSign));
        String authorization = String.format("HMAC-SHA256 Credential=%s, SignedHeaders=%s, Signature=%s", credential.get("accessKeyId") + "/" + credentialScope, signedHeadersStr, signature);
        // Step 7: In the request, create an HTTP request instance.
        HttpUriRequest request;
        if("POST".equalsIgnoreCase(method)){
            HttpPost httpPost = new HttpPost("https://" + requestParam.host + requestParam.path + "?" + uri.getRawQuery());
            // Step 8: Write the Signature into the HTTP Header and send the HTTP request.
            // Set the 5 signed HTTP Headers
            httpPost.setEntity(new ByteArrayEntity(body));
            for (Map.Entry<String, String> entry : header.entrySet()) {
                httpPost.setHeader(entry.getKey(), entry.getValue());
            }
            request = httpPost;
        } else if("GET".equalsIgnoreCase(method)){
            HttpGet httpGet = new HttpGet("https://" + requestParam.host + requestParam.path + "?" + uri.getRawQuery());
            for (Map.Entry<String, String> entry : header.entrySet()) {
                httpGet.setHeader(entry.getKey(), entry.getValue());
            }
            request = httpGet;
        } else {
            throw new UnsupportedOperationException();
        }
        request.setHeader("Host", requestParam.host);
        request.setHeader("Content-Type", requestParam.contentType);
        request.setHeader("X-Date", xDate);
        request.setHeader("X-Content-Sha256", xContentSha256);
        request.setHeader("Authorization", authorization);


        CloseableHttpClient httpClient = HttpClients.createDefault();
        byte[] responseBody = null;


        // Send the HTTP request.
        try {
            CloseableHttpResponse response = httpClient.execute(request);
            HttpEntity entity = response.getEntity();
            responseBody = EntityUtils.toByteArray(entity);
            EntityUtils.consume(entity);
        } catch (IOException e) {
            e.printStackTrace();
        }
        return responseBody;
    }


    public static void main(String[] args) throws URISyntaxException {
        // (POST request) Call UpdateZone API
        HashMap<String, Object> requestBody = new HashMap<>();
        requestBody.put("ZID", 100);
        requestBody.put("Remark", "example");
        byte[] updateZoneResult = request("POST", new HashMap<>(), new HashMap<>(), AK, SK, "UpdateZone", JSON.toJSONBytes(requestBody));
        // Print the output result
        System.out.println("response body:");
        if (updateZoneResult != null) {
            System.out.println(new String(updateZoneResult, StandardCharsets.UTF_8));
        } else {
            System.out.println("null");
        }


        // (GET request) Call CheckZone API
        HashMap<String, String> query = new HashMap<>();
        query.put("ZoneName", "example.com");
        byte[] checkZoneResult = request("GET", query, new HashMap<>(), AK, SK, "CheckZone", new byte[]{});
        // Print the output result
        System.out.println("response body:");
        if (checkZoneResult != null) {
            System.out.println(new String(checkZoneResult, StandardCharsets.UTF_8));
        } else {
            System.out.println("null");
        }
    }
}
```


<span id="1e47029b"></span>
### Python example code

The following example code demonstrates how to authenticate your request when calling UpdateZone API and CheckZone API.

Before running the example code, you need to [get your Access Key ID and Secret Access Key](https://console.byteplus.com/iam/keymanage). Then, you need to pass the values of your Access Key ID and Secret Access Key into the `AK` variable and `SK` variable in the example code, respectively.

```Python
import datetime
import hashlib
import hmac
import json
from urllib.parse import quote


import requests


Service = "DNS"
Version = "2018-08-01"
Region = "singapore"
Host = "dns.byteplusapi.com"
AK = "ak"
SK = "sk"



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



# Step 1: Prepare auxiliary functions.
# sha256 asymmetric encryption
def hmac_sha256(key: bytes, content: str):
    return hmac.new(key, content.encode("utf-8"), hashlib.sha256).digest()


# sha256 hash algorithm
def hash_sha256(content: str):
    return hashlib.sha256(content.encode("utf-8")).hexdigest()


# Step 2: Create a DNS API request function. The signature calculation process is included in this function.
def request(method, query, header, ak, sk, action, body):
    # Step 3: Create identity proof. The Service and Region fields are fixed. ak and sk represent AccessKeyID and SecretAccessKey respectively.
    # Also initialize the signature structure. Some properties required for signature calculation are also handled here.
    # Initialize identity proof structure
    credential = {
        "access_key_id": ak,
        "secret_access_key": sk,
        "service": Service,
        "region": Region,
    }
    # Initialize signature structure
    request_param = {
        "body": json.dumps(body),
        "host": Host,
        "path": "/",
        "method": method,
        "content_type": "application/json",
        "date": datetime.datetime.utcnow(),
        "query": {"Action": action, "Version": Version, **query},
    }
    # Step 4: Start calculating the signature. Before calculating the signature, prepare the signResult variable to receive the signature result and set some parameters.
    # Initialize signature result structure
    x_date = request_param["date"].strftime("%Y%m%dT%H%M%SZ")
    short_x_date = x_date[:8]
    x_content_sha256 = hash_sha256(request_param["body"])
    sign_result = {
        "Host": request_param["host"],
        "X-Content-Sha256": x_content_sha256,
        "X-Date": x_date,
        "Content-Type": request_param["content_type"],
    }
    # Step 5: Calculate the Signature.
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
    # Step 6: Write the Signature into the HTTP Header and send the HTTP request.
    if method == "POST":
        r = requests.post("https://{}{}".format(request_param["host"], request_param["path"]),
                          headers=header,
                          params=request_param["query"],
                          data=request_param["body"],
                          )
        return r.json()
    if method == "GET":
        r = requests.get("https://{}{}".format(request_param["host"], request_param["path"]),
                          headers=header,
                          params=request_param["query"],
                          data=request_param["body"],
                          )
        return r.json()



if __name__ == "__main__":
    # (POST request) Call UpdateZone API
    request_body = {
        "ZID": 100,
        "Remark": "example",
    }
    update_zone_result = request("POST", {}, {}, AK, SK, "UpdateZone", request_body)
    print(update_zone_result)


    # (GET request) Call CheckZone API
    request_query = {"ZoneName": "example.com"}
    check_zone_result = request("GET", request_query, {}, AK, SK, "CheckZone", {})
    print(check_zone_result)
```


<span id="2c59e9b5"></span>
## Request authentication algorithms

You can provide authentication information using either of the following methods. Method 1 is recommended.

<span id="ed6762a9"></span>
### Method 1: (Recommended) Include authentication information in the request header

You need to include the following parameters in the request header:


|**Parameter Name** |**Data Type** |**Required** |**Description** |**Example** |
|---|---|---|---|---|
|X\-Date |String |Yes |The time when the signature is calculated, represented in UTC. The time precision is in seconds. |`20201103T104027Z` |
|Authorization |String |Yes |The authentication string. This parameter represents a structure. The structure includes `Signature`.<br><br>```Plain```<br>```HMAC-SHA256 Credential = {AccessKey}/{ShortDate}/{Region}/{Service}/{Request}, SignedHeaders={SignedHeaders}, Signature={Signature}```<br> |A structure that includes `Signature`. |


**Sample request**

```HTTP
GET https://dns.byteplusapi.com/?Action=ListZones&Version=2018-08-01

X-Date: 20230116T073702Z
Authorization: HMAC-SHA256 Credential=AKLTMjYxYTZmYWU4ZWYzNGI2NDg8NTUxODE1ZGVhNmIxZmQ/20230116/singapore/DNS/request, SignedHeaders=x-content-sha256;x-date, Signature=5a394ce80456c7cdf989c28bd638807c8ead386eb15dd36e39952f405380aef2
ServiceName: DNS
```


<span id="7d34eb95"></span>
### Method 2: Include authentication information in the query string

You need to include the following query parameters in the query string.


|**Parameter Name** |**Data Type** |**Required** |**Description** |**Example** |
|---|---|---|---|---|
|X\-Date |String |Yes |The time when the signature is calculated, represented in UTC. The time precision is in seconds. |`20201103T104027Z` |
|X\-Algorithm |String |Yes |The algorithm used for signature calculation. The value of this parameter is `HMAC-SHA256`. |`HMAC-SHA256` |
|X\-Credential |String |Yes |The pseudo code structure of `X-Credential` is as follows:<br><br>```Plain```<br>```{AccessKey}/{ShortDate}/{Region}/{Service}/{Request}```<br> |`AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE/20210913/cn-north-1/DNS/request` |
|X\-SignedHeaders |String |Yes |The request header parameters involved in signature calculation. Multiple request header parameters are separated by semicolons (;). These request header parameters are sorted in ascending order based on the parameter names. The definition of `X-SignedHeaders` is the same as that of the `SignedHeaders` parameter. You need to use `X-SignedHeaders` when calculating the parameter value of `CanonicalRequest`.<br><br>In general, the value of `X-SignedHeaders` is `host;x-content-sha256;x-date`. You can also specify any request header parameter as the value of `X-SignedHeaders`. |`host;x-content-sha256;x-date` |
|X\-Signature |String |Yes |Represents a calculated signature. | |


<span id="2d6f4951"></span>
### Parameters in the pseudo code

The table below provides explanations for several parameters used in the pseudo code in this document.


|**Parameter Name** |**Data Type** |**Description** |**Example** |
|---|---|---|---|
|AccessKey |string |Represents the Access Key ID of your account. Refer to [Get Access Key](https://console.byteplus.com/iam/keymanage). |`AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE` |
|RequestDate |string |This parameter is the same as the `X-Date`. |`20210913T081805Z` |
|ShortDate |string |This parameter is the same as the `RequestDate`, but with a precision of day. |`20210913` |
|Region |string |Represents the region where the BytePlus DNS service is located. The value of this parameter is `singapore`. |`singapore` |
|Service |string |Represents the service name of BytePlus DNS. The value of this parameter is `DNS`. |`DNS` |
|SignedHeaders |string |Represents the request header parameters involved in the signature calculation. Multiple request header parameters are separated by semicolons (`;`). These request header parameters are sorted in ascending order based on the parameter names.<br><br>In general, the value of `SignedHeaders` is `host;x-content-sha256;x-date`. You can also specify any request header parameter as the value of `SignedHeaders`. |`host;x-content-sha256;x-date` |
|Algorithm |string |Represents the algorithm used for signature calculation. The value of this parameter is `HMAC-SHA256`. |`HMAC-SHA256` |
|Request |string |This parameter is a constant with the value `request`. |`request` |
