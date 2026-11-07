---
title: "IP address functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/IP-address-functions-2"
---

This topic describes the syntax of IP address functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="1c1a35e7"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For IP addresses outside China, you cannot use the IP_TO_PROVINCE function to query provinces or the IP_TO_PROVIDER function to query the internet service provider (ISP). The latitude and longitude coordinates returned by the IP_TO_GEO function are those of the country where you are located.</div>


* <div data-tips="true" data-tips-type="tip">Limited by the assignment mechanism of IP addresses and the scope of the IP address library, IP address functions may fail to return the location details of a small number of IP addresses or return inaccurate query results.</div>


* <div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>




|Category |Function |Syntax |Description |
|---|---|---|---|
|IPv4 address functions |IP_TO_CITY |IP_TO_CITY(KEY) |Identifies the city to which an IPv4 address belongs, and returns the Chinese name of the city. |
||IP_TO_CITY |IP_TO_CITY(KEY, 'en') |Identifies the city to which an IPv4 address belongs, and returns the administrative division code of the city. |
||IP_TO_CITY_GEO |IP_TO_CITY_GEO(KEY) |Identifies the latitude and longitude of the city to which an IPv4 address belongs. Each city has only one set of coordinates. |
||IP_TO_COUNTRY |IP_TO_COUNTRY(KEY) |Identifies the country or region to which an IPv4 address belongs, and returns the Chinese name of the country or region. |
||IP_TO_COUNTRY |IP_TO_COUNTRY(KEY, 'en') |Identifies the country or region to which an IPv4 address belongs, and returns the code of the country or region. |
||IP_TO_DOMAIN |IP_TO_DOMAIN(KEY) |Verifies whether an IPv4 address is a private or public address. |
||IP_TO_GEO |IP_TO_GEO(KEY) |Identifies the latitude and longitude of the location of an IPv4 address. |
||IP_TO_PROVIDER |IP_TO_PROVIDER(KEY) |Identifies the ISP of an IPv4 address. |
||IP_TO_PROVINCE |IP_TO_PROVINCE(KEY) |Identifies the province to which an IPv4 address belongs, and returns the Chinese name of the province. |
||IP_TO_PROVINCE |IP_TO_PROVINCE(KEY, 'en') |Identifies the province to which an IPv4 address belongs, and returns the administrative division code of the province. |
|IPv4 CIDR block functions |IS_PREFIX_SUBNET_OF |IS_PREFIX_SUBNET_OF(*x*, KEY) |Verifies whether an IPv4 CIDR block is a subnet of a specified CIDR block. |
||IS_SUBNET_OF |IS_SUBNET_OF(*x*, KEY) |Verifies whether an IPv4 address is within a specified CIDR block. |
||IP_SUBNET_RANGE |IP_SUBNET_RANGE(KEY) |Returns the range of an IPv4 CIDR block. |
|IPv6 address functions |IPV6_TO_CITY |IPV6_TO_CITY(KEY) |Identifies the city to which an IPv6 address belongs. |
||IPV6_TO_CITY_GEO |IPV6_TO_CITY_GEO(KEY) |Identifies the longitude and latitude of the city to which an IPv6 address belongs. |
||IPV6_TO_COUNTRY |IPV6_TO_COUNTRY(KEY) |Identifies the country or region to which an IPv6 address belongs. |
||IPV6_TO_DOMAIN |IPV6_TO_DOMAIN(KEY) |Verifies whether an IPv6 address is a private or public address. |
||IPV6_TO_PROVIDER |IPV6_TO_PROVIDER(KEY) |Identifies the ISP of an IPv6 address. |
||IPV6_TO_PROVINCE |IPV6_TO_PROVINCE(KEY) |Identifies the province to which an IPv6 address belongs. |


<span id="IP_TO_CITY"></span>
## IP_TO_CITY

The IP_TO_CITY function identifies the city to which the specified IPv4 address belongs.

<span id="4a1d44ba"></span>
### Function **syntax**


* Syntax format

   * Returns the Chinese name of the city.

      ```SQL
      IP_TO_CITY(KEY)
      ```
      

   * Returns the administrative division code of the city.

      ```SQL
      IP_TO_CITY(KEY,'en')
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv4 address. |
   

* Return value description

   The return value is of the Varchar type.


<span id="bc9d4bd7"></span>
### Example


* Scenario

   Use the `test_ip` field to query the city to which an IP address belongs and the administrative division code of the city.

* Query and analysis statement

   ```SQL
   * | SELECT IP_TO_CITY(test_ip), IP_TO_CITY(test_ip, 'en')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a41fe625fa94b1eb3482b601aee3358~tplv-goo7wpa0wc-image.image) </span>


<span id="00008360"></span>
## IP_TO_CITY_GEO

The IP_TO_CITY_GEO function identifies the latitude and longitude of the city to which the specified IPv4 address belongs. Each city has only one set of coordinates.

<span id="e4f13db2"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IP_TO_CITY_GEO(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv4 address. |
   

* Return value description

   The return value is of the Varchar type. Format: `latitude,longitude`.


<span id="0de2d1b2"></span>
### Example


* Scenario

   Use the `test_ip` field to query the latitude and longitude of the city to which an IP address belongs.

* Query and analysis statement

   ```SQL
   * | SELECT IP_TO_CITY_GEO(test_ip)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73773dbce69c4ef9adf9ecd22d83ae38~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="9f68bee4"></span>
## IP_TO_COUNTRY

The IP_TO_COUNTRY function identifies the country or region to which the specified IPv4 address belongs.

<span id="92c0f8b7"></span>
### Function **syntax**


* Syntax format

   * Returns the Chinese name of the country or region.

      ```SQL
      IP_TO_COUNTRY(KEY)
      ```
      

   * Returns the code of a country or a region.

      ```SQL
      IP_TO_COUNTRY(KEY,'en')
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv4 address. |
   

* Return value description

   The return value is of the Varchar type.


<span id="4e942bf1"></span>
### Example


* Scenario

   Use the `test_ip` field to query the Chinese name of a country or a region to which an IP address belongs and the code of the country or region.

* Query and analysis statement

   ```SQL
   * | SELECT IP_TO_COUNTRY(test_ip),IP_TO_COUNTRY(test_ip,'en')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b64de7b15b3c4707941f81cd4e9a3b5c~tplv-goo7wpa0wc-image.image) </span>


<span id="2994f174"></span>
## IP_TO_DOMAIN

The IP_TO_DOMAIN function verifies whether the specified IPv4 address is a private or public address.

<span id="8c5f74db"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IP_TO_DOMAIN(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv4 address. |
   

* Return value description

   The return value is intranet or internet.

   * intranet: indicates a private address.

   * internet: indicates a public address.


<span id="a72002f6"></span>
### Example


* Scenario

   Use the `test_ip` field to query whether an IP address is a private or public address.

* Query and analysis statement

   ```SQL
   * | SELECT IP_TO_DOMAIN(test_ip)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/374850991d4341188882a660dcdf9829~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="367052dd"></span>
## IP_TO_GEO

The IP_TO_GEO function identifies the longitude and latitude of the location of the specified IPv4 address.

<span id="3ef1531f"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IP_TO_GEO(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv4 address. |
   

* Return value description

   The return value is of the Varchar type. Format: `latitude,longitude`.


<span id="4c62819a"></span>
### Example


* Scenario

   Use the `test_ip` field to query the latitude and longitude of the location of the IP address.

* Query and analysis statement

   ```SQL
   * | SELECT IP_TO_GEO(test_ip)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b52c93983ca54e1482b7bb959de8fb96~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="7886a2f6"></span>
## IP_TO_PROVIDER

The IP_TO_PROVIDER function identifies the ISP of the specified IPv4 address.

<span id="56e54796"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IP_TO_PROVIDER(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv4 address. |
   

* Return value description

   The return value is of the Varchar type.


<span id="b1c590cc"></span>
### Example


* Scenario

   Use the `test_ip` field to query the ISP of an IP address.

* Query and analysis statement

   ```SQL
   * | SELECT IP_TO_PROVIDER(test_ip)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d55891a66b66472c90ed8454a63dc157~tplv-goo7wpa0wc-image.image) </span>


<span id="521aaa8a"></span>
## IP_TO_PROVINCE

The IP_TO_PROVINCE identifies the province to which the specified IPv4 address belongs.

<span id="d9bdbd90"></span>
### Function **syntax**


* Syntax format

   * Returns the Chinese name of the province.

      ```SQL
      IP_TO_PROVINCE(KEY)
      ```
      

   * Returns the administrative division code of the province.

      ```SQL
      IP_TO_PROVINCE(KEY,'en')
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv4 address. |
   

* Return value description

   The return value is of the Varchar type.


<span id="eada371f"></span>
### Example


* Scenario

   Use the `test_ip` field to query the province to which an IP address belongs and the administrative division code of the province.

* Query and analysis statement

   ```SQL
   * | SELECT IP_TO_PROVINCE(test_ip), IP_TO_PROVINCE(test_ip,'en') 
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d350b6733f14d53943757981c7e8c52~tplv-goo7wpa0wc-image.image) </span>


<span id="7e9b4836"></span>
## IS_PREFIX_SUBNET_OF

The IS_PREFIX_SUBNET_OF function verifies whether the specified IPv4 CIDR block is a subnet of a specified CIDR block.

<span id="c84dd326"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IS_PREFIX_SUBNET_OF(x, KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |An IPv4 CIDR block. |
   |KEY |A field or an expression. The value is an IPv4 CIDR block.<br><br>Verify whether this CIDR block is a subnet of the x CIDR block. |
   

* Return value description

   The return value is of the Boolean type.


<span id="e21f2603"></span>
### Example


* Scenario

   Verify whether the CIDR block that contains the value of the `test_ip` field is a subnet of `192.168.0.1/24`.

* Query and analysis statement

   ```SQL
   * | SELECT IS_PREFIX_SUBNET_OF('192.168.0.1/24',CONCAT(test_ip,'/24'))
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78818ba5d3414a64bba0eb7e250b527e~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="939bf017"></span>
## IS_SUBNET_OF

The IS_SUBNET_OF function verifies whether the IPv4 address is within a specified CIDR block.

<span id="1e3b35c3"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IS_SUBNET_OF(x, KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |An IPv4 CIDR block. |
   |KEY |A field or an expression. The value is an IPv4 address.<br><br>Verify whether this IP address is in the x CIDR block. |
   

* Return value description

   The return value is of the Boolean type.


<span id="9fd1583c"></span>
### Example


* Scenario

   Verify whether the value of the `test_ip` field is in `192.168.0.1/24`.

* Query and analysis statement

   ```SQL
   * | SELECT IS_SUBNET_OF('192.168.0.1/24',test_ip)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6e155462e87463daae6ec74958e2703~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="2777d1f2"></span>
## IP_SUBNET_RANGE

The IP_SUBNET_RANGE function returns the range of an IPv4 CIDR block.

<span id="6930f861"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IP_SUBNET_RANGE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv4 CIDR block. |
   

* Return value description

   The return value is of the JSON type.


<span id="347f5a42"></span>
### Example


* Scenario

   Get the range of the IPv4 CIDR block that contains the value of the `test_ip` field.

* Query and analysis statement

   ```SQL
   * | SELECT IP_SUBNET_RANGE(CONCAT(test_ip,'/24'))
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4833065485f04d8ebdd8b47f33a10a51~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="e79bf226"></span>
## IPV6_TO_CITY

The IPV6_TO_CITY function identifies the city to which the specified IPv6 address belongs.

<span id="1b352787"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IPV6_TO_CITY(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv6 address. |
   

* Return value description

   The return value is of the Varchar type.


<span id="b7a694cd"></span>
### Example


* Scenario

   Use the `test_ip` field to query the city to which an IP address belongs.

* Query and analysis statement

   ```SQL
   * | SELECT IPV6_TO_CITY(test_ip)  
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51443f7339df49f5ba520a633c775ca9~tplv-goo7wpa0wc-image.image) </span>


<span id="64bdec9b"></span>
## IPV6_TO_CITY_GEO

The IPV6_TO_CITY_GEO function identifies the latitude and longitude of the city to which the specified IPv6 address belongs.

<span id="e1a89c9d"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IPV6_TO_CITY_GEO(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv6 address. |
   

* Return value description

   The return value is of the Varchar type. Format: `latitude,longitude`.


<span id="060407a1"></span>
### Example


* Scenario

   Use the `test_ip` field to query the latitude and longitude of the city to which an IP address belongs.

* Query and analysis statement

   ```SQL
   * | SELECT IPV6_TO_CITY_GEO(test_ip) 
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6810504b04b9486fa96bed1ee5ce72f3~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="2cf609d9"></span>
## IPV6_TO_COUNTRY

The IPV6_TO_COUNTRY function identifies the country or region to which the specified IPv6 address belongs.

<span id="528b5862"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IPV6_TO_COUNTRY(KEY) 
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv6 address. |
   

* Return value description

   The return value is of the Varchar type.


<span id="c4358af3"></span>
### Example


* Scenario

   Use the `test_ip` field to query the country or region to which an IP address belongs.

* Query and analysis statement

   ```SQL
   * | SELECT IPV6_TO_COUNTRY(test_ip) 
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9dbe258470514155bc9af233cf5f60c8~tplv-goo7wpa0wc-image.image) </span>


<span id="62b641c6"></span>
## IPV6_TO_DOMAIN

The IPV6_TO_DOMAIN function verifies whether the specified IPv6 address is a private or public address.

<span id="66d81723"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IPV6_TO_DOMAIN(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv6 address. |
   

* Return value description

   The return value is intranet or internet.

   * intranet: indicates a private address.

   * internet: indicates a public address.


<span id="53397d5f"></span>
### Example


* Scenario

   Use the `test_ip` field to query whether an IP address is a private or public address.

* Query and analysis statement

   ```SQL
   * | SELECT IPV6_TO_DOMAIN(test_ip)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f68be0ebf23a4b63b40281c0d28cf61b~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="25d934e0"></span>
## IPV6_TO_PROVIDER

The IPV6_TO_PROVIDER function identifies the ISP of an IP address.

<span id="989488aa"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IPV6_TO_PROVIDER(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv6 address. |
   

* Return value description

   The return value is of the Varchar type.


<span id="b3c5e072"></span>
### Example


* Scenario

   Use the `test_ip` field to query the ISP of an IPv6 address.

* Query and analysis statement

   ```SQL
   * | SELECT IPV6_TO_PROVIDER(test_ip)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e69b6effeb724abcbff2c832e2dff188~tplv-goo7wpa0wc-image.image) </span>


<span id="8cf2fdab"></span>
## IPV6_TO_PROVINCE

The IPV6_TO_PROVINCE function identifies the province to which an IPv6 address belongs.

<span id="bc2ce858"></span>
### Function **syntax**


* Syntax format

   ```SQL
   IPV6_TO_PROVINCE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an IPv6 address. |
   

* Return value description

   The return value is of the Varchar type.


<span id="66c1bc7b"></span>
### Example


* Scenario

   Use the `test_ip` field to query the province to which an IP address belongs.

* Query and analysis statement

   ```SQL
   * | SELECT IPV6_TO_PROVINCE(test_ip)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e58c28b15a6b47df864bc795f6eb1590~tplv-goo7wpa0wc-image.image) </span>
