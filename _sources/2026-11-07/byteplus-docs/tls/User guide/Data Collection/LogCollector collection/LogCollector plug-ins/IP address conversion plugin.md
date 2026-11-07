---
title: "IP address conversion plugin"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/IP_address_conversion_plugin"
---

You can use LogCollector's geoip plugin to convert IP addresses into geographic locations (country, province, city, latitude, and longitude).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">LogCollector V2.3.0 and later versions support this plugin. To check the LogCollector version, refer to <a href="https://docs.byteplus.com/docs/tls/install_logCollector_on_a_host#.5p-l55yL6L2v5Lu254mI5pys">Check software version</a>.</div>


<span id="7e63e260"></span>
## Parameter description


|Name |Type |Required |Description |
|---|---|---|---|
|field |String |Yes |Log field awaiting IP address conversion. |
|mmdb_path |String |Yes |GeoIP database path. |
|language |String |No |Language attribute, default is zh\-CN. |
|city_field |String |No |Field storing city information, default is city. |
|province_field |String |No |Field storing province information, default is province. |
|country_field |String |No |The field storing country information, default is country. |
|longitude_field |String |No |The field storing longitude information, default is longitude. |
|latitude_field |String |No |Field storing latitude information, default is latitude. |
|allow_empty_values |Boolean |No |Whether to keep key\-value pairs if a subfield value is empty after parsing the specified `field` value.<br><br><br>* true: keep.<br><br>* false (default): do not keep. |
|allow_overwrite_keys |Boolean |No |If the key specified in `keys` duplicates a key already present in the collection configuration, should the existing key’s corresponding field be overwritten?<br><br><br>* true: overwrite.<br><br>* false (default): if the key duplicates, the LogCollector plugin configuration fails to execute. |


<span id="9b5068b6"></span>
## Configuration example


* Original log

   ```JSON
   "ip" : "**.**.**.**"
   ```
   

* LogCollector plugin configuration

   ```JSON
   {
       "processors": [
           {
               "geoip": {
                   "field": "ip",
                   "mmdb_path": "/usr/local/data/GeoLite2-City_20181002/GeoLite2-City.mmbd",
               }
           }
       ]
   }
   ```
   

* Processing result

   ```YAML
   "ip": "**.**.**.**
   "city": "beijing"
   "province": "BJ"
   "country": "CN"
   "longitude": "116.********"
   "latitude": "40.********"
   ```
