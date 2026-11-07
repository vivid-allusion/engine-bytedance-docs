---
title: "Configure Geographic Roles"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Configure_Geographic_Roles"
---

To display geographic information data, such as country, province, city, and district/county, in a [Map](https://docs.byteplus.com/docs/DataWind/Map)chart, you need to set the dimension field as a geographic role field. This article introduces how to set a field as a geographic role, as well as how to modify the matching relationship.

<span id="_1-概述"></span>
# Feature overview

Because geographic location names in actual data may not always be completely accurate, before using maps, you need to match the geographic role for the geographic location field so that this data can be mapped to the corresponding locations on the map. If the initial matching is incorrect, you can also modify the matching relationship.


* Geographic role settings allow users to customize the matching relationship between geographic location field values and geographic roles.

* Matching relationship modification allows users to modify the matching relationship to resolve cases where the initial matching relationship is inaccurate.


<span id="7398443c"></span>
# Precautions


* A field supports setting only one geographic role. For example, it cannot be set as both "Country/Region" and "Province/Autonomous Region" at the same time.

* Personal fields and parameter fields do not support geographic role settings.


<span id="aaadac8f"></span>
# Prerequisites

Your operation account must have dataset editing permissions to manage geographic role settings for fields. For authorization operations, see [Role Management](https://docs.byteplus.com/docs/DataWind/Role_Management) **.** 

<span id="06ac88f7"></span>
# Set geographic roles


* In the field list area, you can set geographic roles for fields and match field values to geographic roles.

* Optional matches include "Country/Region" (for China maps), "Province/Autonomous Region" (for China maps), "City", "District/County", "Latitude", "Longitude", or "Latitude and Longitude". This method also enables custom matching of geographic roles, overcoming the limitations of automatic parsing.

* Operation: Click the ⋮ next to the corresponding field, then select geographic role. In the pop\-up window, configure the matching relationship between the field value and the geographic role.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d99e2d42f6c4d0db9ccc7a035780d2d~tplv-goo7wpa0wc-image.image) </span>

<span id="55b45f4e"></span>
# Modify matching relationship


* To modify the mapping relationship, click the ⋮ icon next to the corresponding field and select Geographic Role \- Location Mapping.

* Modify the mapping relationship in the popup window.
