---
title: "HTTP Request Sample"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/http_request_sample"
---

<span id="uWA7a4fR"></span>
# Preparatory Instructions (Mandatory Reading)

The content below is a request example for calling the API via HTTP directly (including the signature process), which can be invoked by replacing the key information.

**Step 1 (Mandatory):**  Obtain AK/SK via BytePlus console. Ensure that your BytePlus account has activated the corresponding permissions and relevant policies.


* Replace the `AccessKeyID` and `SecretAccessKey` values in the example.

* Without permission, an error will be reported.


**Step 2 (Skippable in most cases):**  Refer to the `Action` and its corresponding `Version` in the `Request Parameters - Query Parameters` section of the API documentation.


* Replace the `Action` and `Version` values in the example.


**Step 3 (Mandatory):**  Refer to the `Request Parameters - Body Parameters, Request example` sections of the API documentation. Copy the content of the `Request example` to replace the `Request body` section of the sample code.


* Replace the Body parameter in the example.


**Step4:**  Simply run the program to debug. Once testing and debugging are completed successfully, it may be integrated into the project as needed. (Directly copying the code as\-is is not recommended; instead, it is advisable to adapt it independently or update the relevant package.)

&nbsp;

<span id="mCcWCrrG"></span>
# **Call Example**

<span id="sCd6eEZX"></span>
## **Java**

```Java
package com.byteplus.example.cv;

import com.alibaba.fastjson.JSONObject;
import com.google.common.io.ByteStreams;
import com.volcengine.helper.Utils;
import org.apache.commons.codec.binary.Hex;
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.URL;
import java.nio.ByteBuffer;
import java.nio.charset.Charset;
import java.nio.charset.StandardCharsets;
import java.security.MessageDigest;
import java.text.SimpleDateFormat;
import java.util.*;

/**
 * Copyright (year) BytePlus Technology Ltd.
 * <p>
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 * <p>
 * http://www.apache.org/licenses/LICENSE-2.0
 * <p>
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
public class Sign {
    private static final BitSet URLENCODER = new BitSet(256);
    private static final String CONST_ENCODE = "0123456789ABCDEF";
    public static final Charset UTF_8 = StandardCharsets.UTF_8;
    private final String region;
    private final String service;
    private final String schema;
    private final String host;
    private final String path;
    private final String ak;
    private final String sk;

    static {
        int i;
        for (i = 97; i <= 122; ++i) {
            URLENCODER.set(i);
        }
        for (i = 65; i <= 90; ++i) {
            URLENCODER.set(i);
        }
        for (i = 48; i <= 57; ++i) {
            URLENCODER.set(i);
        }
        URLENCODER.set('-');
        URLENCODER.set('_');
        URLENCODER.set('.');
        URLENCODER.set('~');
    }
    
    public static void main(String[] args) throws Exception {
        // AK,SK information in BytePlus console, Note there is == at end of the sk.
        String AccessKeyID = "AK*****";
        String SecretAccessKey = "******==";
        // Request Domain
        String endpoint = "cv.byteplusapi.com";
        String path = "/"; // path，doesn't include Query
        // Request interface information
        String service = "cv";
        String region = "ap-singapore-1";
        String schema = "https";
        Sign sign = new Sign(region, service, schema, endpoint, path, AccessKeyID, SecretAccessKey);
        // Please refer to the Query parameters in interface documentation.
        String action = "CVSubmitTask";
        String version = "2024-06-06";
        Date date = new Date();
        // Pleaer refer to Body parameters in interface documentation.
        JSONObject req=new JSONObject();
        req.put("req_key","xxx");
        req.put("image_url","xxx");
        //ArrayList<String> imageUrls = new ArrayList<String>();
        //imageUrls.add("******");        
        //req.put("prompt","******");

        sign.doRequest("POST", new HashMap(), req.toJSONString().getBytes(), date, action, version);
    }

    public Sign(String region, String service, String schema, String host, String path, String ak, String sk) {
        this.region = region;
        this.service = service;
        this.host = host;
        this.schema = schema;
        this.path = path;
        this.ak = ak;
        this.sk = sk;
    }

    public void doRequest(String method, Map<String, String> queryList, byte[] body,
                          Date date, String action, String version) throws Exception {
        if (body == null) {
            body = new byte[0];
        }
        String xContentSha256 = hashSHA256(body);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyyMMdd'T'HHmmss'Z'");
        sdf.setTimeZone(TimeZone.getTimeZone("GMT"));
        String xDate = sdf.format(date);
        String shortXDate = xDate.substring(0, 8);
        String contentType = "application/json";
        String signHeader = "host;x-date;x-content-sha256;content-type";

        SortedMap<String, String> realQueryList = new TreeMap<>(queryList);
        realQueryList.put("Action", action);
        realQueryList.put("Version", version);
        StringBuilder querySB = new StringBuilder();
        for (String key : realQueryList.keySet()) {
            querySB.append(signStringEncoder(key)).append("=").append(signStringEncoder(realQueryList.get(key))).append("&");
        }
        querySB.deleteCharAt(querySB.length() - 1);

        String canonicalStringBuilder = method + "\n" + path + "\n" + querySB + "\n" +
                "host:" + host + "\n" +
                "x-date:" + xDate + "\n" +
                "x-content-sha256:" + xContentSha256 + "\n" +
                "content-type:" + contentType + "\n" +
                "\n" +
                signHeader + "\n" +
                xContentSha256;

        System.out.println(canonicalStringBuilder);

        String hashcanonicalString = hashSHA256(canonicalStringBuilder.getBytes());
        String credentialScope = shortXDate + "/" + region + "/" + service + "/request";
        String signString = "HMAC-SHA256" + "\n" + xDate + "\n" + credentialScope + "\n" + hashcanonicalString;

        byte[] signKey = genSigningSecretKeyV4(sk, shortXDate, region, service);
//        String signature = HexFormat.of().formatHex(hmacSHA256(signKey, signString));
        String signature = Hex.encodeHexString(Utils.hmacSHA256(signKey, signString));

        URL url = new URL(schema + "://" + host + path + "?" + querySB);

        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setRequestMethod(method);
        conn.setRequestProperty("Host", host);
        conn.setRequestProperty("X-Date", xDate);
        conn.setRequestProperty("X-Content-Sha256", xContentSha256);
        conn.setRequestProperty("Content-Type", contentType);
        conn.setRequestProperty("Authorization", "HMAC-SHA256" +
                " Credential=" + ak + "/" + credentialScope +
                ", SignedHeaders=" + signHeader +
                ", Signature=" + signature);
        if (!Objects.equals(conn.getRequestMethod(), "GET")) {
            conn.setDoOutput(true);
            OutputStream os = conn.getOutputStream();
            os.write(body);
            os.flush();
            os.close();
        }
        conn.connect();

        int responseCode = conn.getResponseCode();

        InputStream is;
        if (responseCode == 200) {
            is = conn.getInputStream();
        } else {
            is = conn.getErrorStream();
        }
        String responseBody = new String(ByteStreams.toByteArray(is));
        is.close();

        System.out.println(responseCode);
        System.out.println(responseBody);
    }
    
    private String signStringEncoder(String source) {
        if (source == null) {
            return null;
        }
        StringBuilder buf = new StringBuilder(source.length());
        ByteBuffer bb = UTF_8.encode(source);
        while (bb.hasRemaining()) {
            int b = bb.get() & 255;
            if (URLENCODER.get(b)) {
                buf.append((char) b);
            } else if (b == 32) {
                buf.append("%20");
            } else {
                buf.append("%");
                char hex1 = CONST_ENCODE.charAt(b >> 4);
                char hex2 = CONST_ENCODE.charAt(b & 15);
                buf.append(hex1);
                buf.append(hex2);
            }
        }
        
        return buf.toString();
    }

    public static String hashSHA256(byte[] content) throws Exception {
        try {
            MessageDigest md = MessageDigest.getInstance("SHA-256");


            return Hex.encodeHexString(md.digest(content));
        } catch (Exception e) {
            throw new Exception(
                    "Unable to compute hash while signing request: "
                            + e.getMessage(), e);
        }
    }

    public static byte[] hmacSHA256(byte[] key, String content) throws Exception {
        try {
            Mac mac = Mac.getInstance("HmacSHA256");
            mac.init(new SecretKeySpec(key, "HmacSHA256"));
            return mac.doFinal(content.getBytes());
        } catch (Exception e) {
            throw new Exception(
                    "Unable to calculate a request signature: "
                            + e.getMessage(), e);
        }
    }

    private byte[] genSigningSecretKeyV4(String secretKey, String date, String region, String service) throws Exception {
        byte[] kDate = hmacSHA256((secretKey).getBytes(), date);
        byte[] kRegion = hmacSHA256(kDate, region);
        byte[] kService = hmacSHA256(kRegion, service);
        return hmacSHA256(kService, "request");
    }
}
```


<span id="L2X5QjhE"></span>
## Golang

```Go
/*
Copyright (year) BytePlus Technology Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
*/
package main

import (
        "bytes"
        "crypto/hmac"
        "crypto/sha256"
        "encoding/hex"
        "encoding/json"
        "fmt"
        "log"
        "net/http"
        "net/http/httputil"
        "net/url"
        "strings"
        "time"
)

const (
        // AK,SK information in BytePlus console, Note there is == at end of the sk.
        AccessKeyID     = "AK*****"
        SecretAccessKey = "*****=="

        // Request Domain
        Addr = "https://cv.byteplusapi.com"
        Path = "/" // path，doesn't include Query

        // request interface information
        Service = "cv"
        Region  = "ap-singapore-1"
        
        // Please refer to the Query parameters in interface documentation.
        Action  = "CVSubmitTask"
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

func doRequest(method string, queries url.Values, body []byte) ([]byte, int, error) {
        // 1. Construct request
        queries.Set("Action", Action)
        queries.Set("Version", Version)
        requestAddr := fmt.Sprintf("%s%s?%s", Addr, Path, queries.Encode())
        log.Printf("request addr: %s\n", requestAddr)

        request, err := http.NewRequest(method, requestAddr, bytes.NewBuffer(body))
        if err != nil {
                return nil, 0, fmt.Errorf("bad request: %w", err)
        }

        // 2. Construct signature content
        now := time.Now()
        date := now.UTC().Format("20060102T150405Z")
        authDate := date[:8]
        request.Header.Set("X-Date", date)

        payload := hex.EncodeToString(hashSHA256(body))
        request.Header.Set("X-Content-Sha256", payload)
        request.Header.Set("Content-Type", "application/json")

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

        // 3. Construct signature head
        signedKey := getSignedKey(SecretAccessKey, authDate, Region, Service)
        signature := hex.EncodeToString(hmacSHA256(signedKey, signString))
        log.Printf("signature: %s\n", signature)

        authorization := "HMAC-SHA256" +
                " Credential=" + AccessKeyID + "/" + credentialScope +
                ", SignedHeaders=" + strings.Join(signedHeaders, ";") +
                ", Signature=" + signature

        request.Header.Set("Authorization", authorization)
        log.Printf("authorization: %s\n", authorization)

        // 4. Print request, send request
        requestRaw, err := httputil.DumpRequest(request, true)
        if err != nil {
                return nil, 0, fmt.Errorf("dump request err: %w", err)
        }

        log.Printf("request:\n%s\n", string(requestRaw))

        response, err := http.DefaultClient.Do(request)
        if err != nil {
                return nil, 0, fmt.Errorf("do request err: %w", err)
        }
        // 5. Print response
        responseRaw, err := httputil.DumpResponse(response, true)
        if err != nil {
                return nil, 0, fmt.Errorf("dump response err: %w", err)
        }
        respStr := strings.ReplaceAll(string(responseRaw), "\\u0026", "&")
        log.Printf("response:\n%s\n", respStr)
        return requestRaw, response.StatusCode, err
}

func main() {
        // Pleaer refer to Body parameters in interface documentation.
        reqBody := map[string]interface{}{
                "req_key": "*****",
                "image_url": "*****",
        }

        reqBodyStr, _ := json.Marshal(reqBody)
        _, _, _ = doRequest("POST", url.Values{}, reqBodyStr)
}
```


<span id="118Fl5vY"></span>
## Python

```Python
import json
import sys
import os
import base64
import datetime
import hashlib
import hmac
import requests


method = 'POST'
host = 'cv.byteplusapi.com'
region = 'ap-singapore-1'
endpoint = 'https://cv.byteplusapi.com'
service = 'cv'

def sign(key, msg):
    return hmac.new(key, msg.encode('utf-8'), hashlib.sha256).digest()

def getSignatureKey(key, dateStamp, regionName, serviceName):
    kDate = sign(key.encode('utf-8'), dateStamp)
    kRegion = sign(kDate, regionName)
    kService = sign(kRegion, serviceName)
    kSigning = sign(kService, 'request')
    return kSigning

def formatQuery(parameters):
    request_parameters_init = ''
    for key in sorted(parameters):
        request_parameters_init += key + '=' + parameters[key] + '&'
    request_parameters = request_parameters_init[:-1]
    return request_parameters

def signV4Request(access_key, secret_key, service, req_query, req_body):
    if access_key is None or secret_key is None:
        print('No access key is available.')
        sys.exit()

    t = datetime.datetime.utcnow()
    current_date = t.strftime('%Y%m%dT%H%M%SZ')
    # current_date = '20210818T095729Z'
    datestamp = t.strftime('%Y%m%d')  # Date w/o time, used in credential scope
    canonical_uri = '/'
    canonical_querystring = req_query
    signed_headers = 'content-type;host;x-content-sha256;x-date'
    payload_hash = hashlib.sha256(req_body.encode('utf-8')).hexdigest()
    content_type = 'application/json'
    canonical_headers = 'content-type:' + content_type + '\n' + 'host:' + host + \
        '\n' + 'x-content-sha256:' + payload_hash + \
        '\n' + 'x-date:' + current_date + '\n'
    canonical_request = method + '\n' + canonical_uri + '\n' + canonical_querystring + \
        '\n' + canonical_headers + '\n' + signed_headers + '\n' + payload_hash
    # print(canonical_request)
    algorithm = 'HMAC-SHA256'
    credential_scope = datestamp + '/' + region + '/' + service + '/' + 'request'
    string_to_sign = algorithm + '\n' + current_date + '\n' + credential_scope + '\n' + hashlib.sha256(
        canonical_request.encode('utf-8')).hexdigest()
    # print(string_to_sign)
    signing_key = getSignatureKey(secret_key, datestamp, region, service)
    # print(signing_key)
    signature = hmac.new(signing_key, (string_to_sign).encode(
        'utf-8'), hashlib.sha256).hexdigest()
    # print(signature)

    authorization_header = algorithm + ' ' + 'Credential=' + access_key + '/' + \
        credential_scope + ', ' + 'SignedHeaders=' + \
        signed_headers + ', ' + 'Signature=' + signature
    # print(authorization_header)
    headers = {'X-Date': current_date,
               'Authorization': authorization_header,
               'X-Content-Sha256': payload_hash,
               'Content-Type': content_type
               }
    # print(headers)

    # ************* SEND THE REQUEST *************
    request_url = endpoint + '?' + canonical_querystring

    print('\nBEGIN REQUEST++++++++++++++++++++++++++++++++++++')
    print('Request URL = ' + request_url)
    try:
        r = requests.post(request_url, headers=headers, data=req_body)
    except Exception as err:
        print(f'error occurred: {err}')
        raise
    else:
        print('\nRESPONSE++++++++++++++++++++++++++++++++++++')
        print(f'Response code: {r.status_code}\n')
        # Replace \u0026 with &
        resp_str = r.text.replace("\\u0026", "&")
        print(f'Response body: {resp_str}\n')


if __name__ == "__main__":
    # AK,SK information in BytePlus console, Note there is == at end of the sk.
    access_key = 'AK*****'
    secret_key = '*****=='

    # Please refer to the Query parameters in interface documentation.
    query_params = {
        'Action': 'CVSubmitTask',
        'Version': '2024-06-06',
    }
    formatted_query = formatQuery(query_params)

    # Pleaer refer to Body parameters in interface documentation.
    body_params = {
        "req_key": "******",
        "image_url": "*****",
        # ......
    }
    formatted_body = json.dumps(body_params)
    
    signV4Request(access_key, secret_key, service,
                  formatted_query, formatted_body)
```


<span id="oQHxz375"></span>
## PHP

```PHP
<?php
/**
 * Copyright (year) BytePlus Technology Ltd.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 * http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
require('../vendor/autoload.php');
// Need to install composer（https://getcomposer.org/doc/00-intro.md），and install GuzzleHttp， composer require guzzlehttp/guzzle:^7.0
use GuzzleHttp\Client;
use GuzzleHttp\Exception\GuzzleException;

// Basic information to access BytePlus
$Host = "cv.byteplusapi.com";
$ContentType = "application/json";
$Service = "cv";
$Region = "ap-singapore-1";

/**
 * @throws GuzzleException
 */
// Step1：create API request function。Signature calculation is included in this function
function request($method, $query, $header, $ak, $sk, $action, $version, $body)
{
    // Step 2：Create credential。The Service and Region is fixed。ak and sk is
    // AccessKeyID and SecretAccessKey。Need to initialize the signature structure. Some parameters required in Signature calculation is handled here.
    // initialize the credential structure
    global $Service, $Region, $Host, $ContentType;
    $credential = [
        'accessKeyId' => $ak,
        'secretKeyId' => $sk,
        'service' => $Service,
        'region' => $Region,
    ];
    // initialize the signature structure
    $query = array_merge($query, [
        'Action' => $action,
        'Version' => $version
    ]);
    ksort($query);
    $requestParam = [
        // body is the http request body
        'body' => $body,
        'host' => $Host,
        'path' => '/',
        'method' => $method,
        'contentType' => $ContentType,
        'date' => gmdate('Ymd\THis\Z'),
        'query' => $query
    ];
    // Step3：Then we will start to calculate Signature。Before calculate the signature, please prepare the signResult used to receive the signature，and set parameters。
    // initilize signature structure
    $xDate = $requestParam['date'];
    $shortXDate = substr($xDate, 0, 8);
    $xContentSha256 = hash('sha256', $requestParam['body']);
    $signResult = [
        'Host' => $requestParam['host'],
        'X-Content-Sha256' => $xContentSha256,
        'X-Date' => $xDate,
        'Content-Type' => $requestParam['contentType']
    ];
    // Step4: Calculate signature
    $signedHeaderStr = join(';', ['content-type', 'host', 'x-content-sha256', 'x-date']);
    $canonicalRequestStr = join("\n", [
        $requestParam['method'],
        $requestParam['path'],
        http_build_query($requestParam['query']),
        join("\n", ['content-type:'. $requestParam['contentType'], 'host:'. $requestParam['host'], 'x-content-sha256:'. $xContentSha256, 'x-date:'. $xDate]),
        '',
        $signedHeaderStr,
        $xContentSha256
    ]);
    $hashedCanonicalRequest = hash("sha256", $canonicalRequestStr);
    $credentialScope = join('/', [$shortXDate, $credential['region'], $credential['service'], 'request']);
    $stringToSign = join("\n", ['HMAC-SHA256', $xDate, $credentialScope, $hashedCanonicalRequest]);
    $kDate = hash_hmac("sha256", $shortXDate, $credential['secretKeyId'], true);
    $kRegion = hash_hmac("sha256", $credential['region'], $kDate, true);
    $kService = hash_hmac("sha256", $credential['service'], $kRegion, true);
    $kSigning = hash_hmac("sha256", 'request', $kService, true);
    $signature = hash_hmac("sha256", $stringToSign, $kSigning);
    $signResult['Authorization'] = sprintf("HMAC-SHA256 Credential=%s, SignedHeaders=%s, Signature=%s", $credential['accessKeyId']. '/'. $credentialScope, $signedHeaderStr, $signature);
    $header = array_merge($header, $signResult);
    // Step5: Add Signature into HTTP Header and send HTTP request
    $client = new Client([
        'base_uri' => 'https://'. $requestParam['host'],
        'timeout' => 120.0,
    ]);
    $response = $client->request($method, 'https://'. $requestParam['host']. $requestParam['path'], [
        'headers' => $header,
        'query' => $requestParam['query'],
        'body' => $requestParam['body']
    ]);
    $responseContent = $response->getBody()->getContents();
    // Change \u0026 to &
    $responseContent = str_replace('\u0026', '&', $responseContent);
    return $responseContent;
}
$now = time();
// AK,SK information in BytePlus console, Note there is == at end of the sk.
$AccessKeyID = 'AK*****';
$SecretAccessKey = '*****==';

// Please refer to the Query Parameters in interface documentation.
$action = "CVSubmitTask";
$version = "2024-06-06";

// Please refer to Body Parameters in interface documentation.
$requestBody = [
    "req_key" => "******",
    "image_url" => "*****",
    //......
];
$body = json_encode($requestBody);

try {
    $response = request("POST", [], [], $AccessKeyID, $SecretAccessKey, $action, $version, $body);
    print_r($response);
} catch (GuzzleException $e) {
    print_r($e->getResponse()->getBody()->getContents() . "\n");
}
```


<span id="6GcHi9uZ"></span>
## Node.js

```JavaScript
"use strict";
/*
Copyright (year) BytePlus Technology Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

     http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
*/
const crypto = require("crypto");
const util = require("util");
const url = require("url");
//if node.js version < 18.0.0 might require node-fetch
//const fetch = require("node-fetch");
const qs = require("querystring");
const debuglog = util.debuglog('signer');


/**
 *  header key which doesn't need sign
 */
const HEADER_KEYS_TO_IGNORE = new Set([
    "authorization",
    "content-type",
    "content-length",
    "user-agent",
    "presigned-expires",
    "expect",
]);

// do request example
async function doRequest() {
    try {

    // ***Modification required*** 
    // Please refer to Body Parameters in interface documentation.
    const requestBody = {
        "req_key" : "xxxxx",
        "image_url": "xxxxx" 
    };

    const bodySha = getBodySha(JSON.stringify(requestBody));

    const signParams = {
        headers: {
            // x-date header is required
            ["X-Date"]: getDateTimeNow(),
            "Content-Type": "application/json",
        },
        method: 'POST',
        
        //***Modification required*** 
        // Please refer to the Query Parameters in interface documentation.
        query: {
            Version: '2024-06-06',
            Action: 'CVSubmitTask',
        },

        //***Modification required*** 
        // Need to fulfill the ak,sk get from BytePlus console. SK ends with ==.
        accessKeyId: 'AKxxxxx',
        secretAccessKey: 'xxxxxx==',
        
        
        serviceName: 'cv',
        region: 'ap-singapore-1',
        bodySha: bodySha,
    };

    // Check query object， in case query is undefined.
    for (const [key, val] of Object.entries(signParams.query)) {
        if (val === undefined || val === null) {
            signParams.query[key] = '';
        }
    }
    const authorization = sign(signParams);

    //BytePlus cv URL
    const requestUrl = `https://cv.byteplusapi.com/?${qs.stringify(signParams.query)}`;
    const res = await fetch(requestUrl, {
        headers: {
            ...signParams.headers,
            'Authorization': authorization,
        },
        method: signParams.method,
        body: JSON.stringify(requestBody),
    });
    const responseText = await res.text();
    console.log(responseText);
} catch (error) {
    console.error("Request failed:", error.message);
    // print error details
    console.error("Error message:", error.stack);
  }
}

doRequest();


function sign(params) {
    const {
        headers = {},
        query = {},
        region = '',
        serviceName = '',
        method = '',
        pathName = '/',
        accessKeyId = '',
        secretAccessKey = '',
        needSignHeaderKeys = [],
        bodySha,
    } = params;
    const datetime = headers["X-Date"];
    const date = datetime.substring(0, 8); // YYYYMMDD
    
    const [signedHeaders, canonicalHeaders] = getSignHeaders(headers, needSignHeaderKeys);
    const canonicalRequest = [
        method.toUpperCase(),
        pathName,
        queryParamsToString(query) || '',
        `${canonicalHeaders}\n`,
        signedHeaders,
        bodySha || hash(''),
    ].join('\n');
    const credentialScope = [date, region, serviceName, "request"].join('/');
    
    // Create signature string
    const stringToSign = ["HMAC-SHA256", datetime, credentialScope, hash(canonicalRequest)].join('\n');
    // Calculate signature
    const kDate = hmac(secretAccessKey, date);
    const kRegion = hmac(kDate, region);
    const kService = hmac(kRegion, serviceName);
    const kSigning = hmac(kService, "request");
    const signature = hmac(kSigning, stringToSign).toString('hex');
    debuglog('--------CanonicalString:\n%s\n--------SignString:\n%s', canonicalRequest, stringToSign);

    return [
        "HMAC-SHA256",
        `Credential=${accessKeyId}/${credentialScope},`,
        `SignedHeaders=${signedHeaders},`,
        `Signature=${signature}`,
    ].join(' ');
}

function hmac(secret, s) {
    return crypto.createHmac('sha256', secret).update(s, 'utf8').digest();
}

function hash(s) {
    return crypto.createHash('sha256').update(s, 'utf8').digest('hex');
}

function queryParamsToString(params) {
    return Object.keys(params)
        .sort()
        .map((key) => {
            const val = params[key];
            if (typeof val === 'undefined' || val === null) {
                return undefined;
            }
            const escapedKey = uriEscape(key);
            if (!escapedKey) {
                return undefined;
            }
            if (Array.isArray(val)) {
                return `${escapedKey}=${val.map(uriEscape).sort().join(`&${escapedKey}=`)}`;
            }
            return `${escapedKey}=${uriEscape(val)}`;
        })
        .filter((v) => v)
        .join('&');
}

function getSignHeaders(originHeaders, needSignHeaders) {
    function trimHeaderValue(header) {
        return header.toString?.().trim().replace(/\s+/g, ' ') ?? '';
    }

    let h = Object.keys(originHeaders);
    // Filter based on needSignHeaders
    if (Array.isArray(needSignHeaders)) {
        const needSignSet = new Set([...needSignHeaders, 'x-date', 'host'].map((k) => k.toLowerCase()));
        h = h.filter((k) => needSignSet.has(k.toLowerCase()));
    }
    // Filter based on ignore headers
    h = h.filter((k) => !HEADER_KEYS_TO_IGNORE.has(k.toLowerCase()));
    const signedHeaderKeys = h
        .slice()
        .map((k) => k.toLowerCase())
        .sort()
        .join(';');
    const canonicalHeaders = h
        .sort((a, b) => (a.toLowerCase() < b.toLowerCase() ? -1 : 1))
        .map((k) => `${k.toLowerCase()}:${trimHeaderValue(originHeaders[k])}`)
        .join('\n');
    return [signedHeaderKeys, canonicalHeaders];
}

function uriEscape(str) {
    try {
        return encodeURIComponent(str)
            .replace(/[^A-Za-z0-9_.~\-%]+/g, escape)
            .replace(/[*]/g, (ch) => `%${ch.charCodeAt(0).toString(16).toUpperCase()}`);
    } catch (e) {
        return '';
    }
}

function getDateTimeNow() {
    const now = new Date();
    return now.toISOString().replace(/[:-]|\.\d{3}/g, '');
}

// Get body sha256
function getBodySha(body) {
    const hash = crypto.createHash('sha256');
    if (typeof body === 'string') {
        hash.update(body);
    } else if (body instanceof url.URLSearchParams) {
        hash.update(body.toString());
    } else if (util.isBuffer(body)) {
        hash.update(body);
    }
    return hash.digest('hex');
}
```
