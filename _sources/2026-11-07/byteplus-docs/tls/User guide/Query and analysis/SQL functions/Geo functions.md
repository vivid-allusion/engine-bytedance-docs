---
title: "Geo functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Geo-functions"
---

This topic describes the syntax of a geo function supported by Torch Log Service (TLS) and offers an example on how to use the function.

<span id="97ffce71"></span>
### List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Syntax |Description |
|---|---|---|
|GEOHASH |GEOHASH(KEY) |Encodes latitudes and longitudes using the Geohash algorithm. |


<span id="1505d35d"></span>
### GEOHASH

The GEOHASH function encodes latitudes and longitudes in Geohash.

<span id="895cee24"></span>
#### Function **syntax**


* Syntax format

   ```SQL
   GEOHASH(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is of the String type. The value specifies a longitude and a latitude. Example: IP_TO_GEO(longitude,latitude). |
   

* Return value description

   The return value is of the String type.


<span id="9855121b"></span>
#### Example


* Scenario

   The IP_TO_GEO function is used to analyze the longitude and latitude of the IP address related to the `test_ip` field. Then, the GEOHASH function is used to encode the longitude and latitude.

* Query and analysis statement

   ```SQL
   * | SELECT GEOHASH(IP_TO_GEO(test_ip))
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f76441b2211442188cdc903fd021251~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
