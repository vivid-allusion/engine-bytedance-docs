---
title: "IP address parsing functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/ip_address_parsing_functions"
---

<span id="geo-parse-函数"></span>
## geo_parse function

This function parses IP addresses into the corresponding location information such as geographical locations and administrative divisions. IPV4 and IPV6 addresses are supported. The location corresponding to an IP address may change.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
geo_parse(ip,fields=fields to be retained,sep=",")
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|ip |String |Yes |/ |/ |Specify one or more IP addresses to be parsed. Separate multiple IP addresses with number signs (#). |
|fields |String |No |city,province,country,city_en,province_en,country_en,isp,lat,lon |/ |Specify fields to be retained in the result generated after the function parses the IP addresses. The following fields are returned by default:<br><br><br>* city: the name of the city.<br><br>* province: the name of the province.<br><br>* country: the name of the country.<br><br>* city_en: the English name of the city.<br><br>* province_en: the English name of the province.<br><br>* country_en: the English name of the country.<br><br>* isp: the name of the internet service provider (ISP).<br><br>* lat: the latitude of the IP address.<br><br>* lon: the longitude of the IP address.<br><br><br>If you want to specify multiple fields, use commas ( , ) to separate them. For example, `fields="city,province"`. |
|sep |String |No |, |Visible characters |If you specify multiple IP addresses for the ip parameter, use this parameter to define the delimiter. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: The function parses an IP address.

* Transformation rule:

   ```python
   f_set("ip_location",geo_parse(v("ip")))
   ```
   

* Sample log:

   ```json
   {
       "ip":"2408:844f:9f31:4e3:31f:7522:xxxx:xxx"
   }
   ```
   

* Transformation result:

   ```json
   {
       "ip":"2408:844f:9f31:4e3:31f:7522:xxxx:xxx",
       "ip_location":{
           "city":"Huanggang",
           "city_en":"Huanggang",
           "country":"China",
           "country_en":"People's Republic of China",
           "isp":"",
           "lat":30.4477xx,
           "lon":114.8793xx,
           "province":"Hubei",
           "province_en":"Hubei"
       }
   }
   ```
   


Example 2:


* Scenario: The function parses multiple IP addresses.

* Transformation rule:

   ```python
   f_set("ip_location",geo_parse(v("ip"),"city,province","#"))
   ```
   

* Sample log:

   ```json
   {
       "ip":"118.115.xx.xxx#183.225.xx.xxx"
   }
   ```
   

* Transformation result:

   ```json
   {
       "ip":"118.115.xx.xxx#183.225.xx.xxx",
       "ip_location":{
           "118.115.xx.xxx":{
               "city":"Neijiang",
               "province":"Sichuan"
           },
           "183.225.xx.xxx":{
               "city":"Honghe",
               "province":"Yunnan"
           }
       }
   }
   ```
