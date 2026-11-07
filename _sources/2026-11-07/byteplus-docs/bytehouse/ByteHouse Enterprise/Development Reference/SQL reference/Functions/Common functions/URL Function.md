---
title: "URL Function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/url-function"
---

All these functions do not follow RFC. They are simplified to the maximum extent to enhance performance.
<span id="url截取函数"></span>
## URL Truncate Function
If there is no content to truncate in the URL, an empty string is returned.
<span id="protocol"></span>
### **protocol**
Returns the protocol of the URL. Examples: http, ftp, mailto, magnet...
<span id="domain"></span>
### **domain**
Retrieve the Domain Name.
<span id="domainwithoutww"></span>
### domainwithoutww
Return the domain name and remove the first 'www.'.
<span id="topleveldomain"></span>
### topLevelDomain
Return to the top-level Domain Name. For example: .ru.
<span id="firstsignificantsubdomain"></span>
### **firstSignificantSubdomain**
Returns the "first significant subdomain". This is not a standard concept and is only used in Yandex.Metrica. If the top-level domain is 'com', 'net', 'org', or 'co', the first significant subdomain is the second-level domain. Otherwise, it returns the third-level domain. For example, firstSignificantSubdomain('https://news.yandex.ru/') = 'yandex' and firstSignificantSubdomain('https://news.yandex.com.tr/') = 'yandex'. Some implementation details may change in the future.
<span id="cuttofirstsignificantsubdomain"></span>
### cutToFirstSignificantSubdomain
Returns the content between the top-level domain and the first significant subdomain (refer to the above content).
For example, `cutToFirstSignificantSubdomain('https://news.yandex.com.tr/') = 'yandex.com.tr'`.
<span id="path"></span>
### **path**
Returns the URL path. For example: `/top/news.html`, without including request parameters.
<span id="pathfull"></span>
### pathFull
Similar to the above, but includes request parameters and fragment. For example: /top/news.html?page=2#comments
<span id="querystring"></span>
### **queryString**
Return the parameter. For example: page=1&lr=213. The parameter does not include a question mark, the #, or any content after the #.
<span id="fragment"></span>
### **fragment**
Returns the fragment identifier of the URL. The fragment does not include a hash (#).
<span id="querystring-andfragment"></span>
### querystring andfragment
Return request parameters and fragment identifiers. For example: page=1#29390.
<span id="extracturlparameter-url-name"></span>
### extractURLParameter(URL,name)
Return the parameter named 'Name' in the URL request parameters. If it does not exist, return an empty string. If there are multiple matches, return the first matching one. This function assumes that the encoding method for parameter names and parameter values in the URL is the same.
<span id="extracturlparameters-url"></span>
### extractURLParameters(URL)
Return an array containing all request parameters of the URL in the form of name=value strings. Do not decode any content.
<span id="extracturlparameternames-url"></span>
### extractURLParameterNames(URL)
Return an array containing the names of all request parameters of the URL. Do not decode any content in any way.
<span id="urlhierarchy-url"></span>
### URLHierarchy(URL)
Return an array containing all segments of the URL split by "/". ？ Will be included in the URL path and request parameters. Consecutive delimiters are counted as one.
<span id="urlpathhierarchy-url"></span>
### Urlpathhierarchy(URL)
Same as above, but the result does not contain the Agreement and Domain Name parts. /element(root) is not included. The function is used to implement the export of a tree-structured URL in Yandex.Metric.
```plaintext
URLPathHierarchy('https://example.com/browse/CONV-6788') =
[
    '/browse/',
    '/browse/CONV-6788'
]
```

<span id="decodeurlcomponent-url"></span>
### decodeURLComponent(URL)
Return the already decoded URL. For example:
```SQL
SELECT decodeURLComponent('http://127.0.0.1:8123/?query=SELECT%201%3B') AS DecodedURL;
```

```plaintext
┌─DecodedURL─────────────────────────────┐
│ http://127.0.0.1:8123/?query=SELECT 1; │
└────────────────────────────────────────┘
```
