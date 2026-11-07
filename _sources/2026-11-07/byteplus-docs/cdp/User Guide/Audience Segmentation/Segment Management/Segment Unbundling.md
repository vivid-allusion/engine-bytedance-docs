---
title: "Segment Unbundling"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Segment_Unbundling"
---

<span id="b422d599"></span>
# 1. Function Overview

Cluster Unpacking supports two types of unpacking: random unpacking and advanced unpacking.

Random unpacking randomly splits according to the number of sub\-packages, while advanced unpacking allows for precise grouping operations based on labels.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59cd035334e247b5963dc3fc512f30fd~tplv-goo7wpa0wc-image.image) </span>

<span id="89359695"></span>
# 2. Application Scenarios

This function is suitable for various business scenarios, meeting personalized marketing and refined operation needs. Examples of advanced unpacking scenarios are as follows:

For example, in a large chain coffee shop, after the headquarters selects specific clusters (such as potential churn customers), using the "advanced unpacking" function, the headquarters can subdivide these potential churn customers into multiple sub\-clusters based on the "store affiliation" label. Then, each store can develop personalized retention strategies for its customer base, such as sending exclusive coupons or inviting them to store events, to improve customer retention.

<span id="a88ffe82"></span>
# 3. Operation Steps

<span id="983be475"></span>
## 2.1 Random Unpacking

Random unpacking supports selecting from 3 methods:


1. Maximum quantity limit restriction, supports configuring the maximum quantity limits of different sub\-packages for splitting

2. Limit the number of packages, support configuring the number of sub\-packages to split, and split them evenly based on the set quantity

3. Split by proportion, support configuring the proportion of the number of sub\-packages to the total quantity, and split accordingly


<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4999405d8720afcbf83cd4d200af5ad3.png" width="2878px" /></div>


After configuration, click the small triangle icon in front of the audience package to expand and view the sub\-packages.

<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7048ff96c93028777d061bc1bdb214dc.png" width="2878px" /></div>


<span id="86f35d0d"></span>
## 2.2 Advanced package splitting

> \*This feature is an add\-on and requires an additional fee.

> \*This feature is controlled by a product switch and is off by default.

> \*The maximum split package limit for this feature is 10


Rule creation, segment grouping, and segmented group upload support advanced package splitting functionality, including:


* Include: specifying tag values as sub\-segments

* Exclusion: Excluding specific tag values, the rest are referred to as subgroups

* Top N Users: The N most frequent user tag values are referred to as subgroups

* Excluded Top N Users: Excluding specific tag values, and the N most frequent user tag values are referred to as subgroups


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75bdf4c44d834480b4b0fb7f98299a01~tplv-goo7wpa0wc-image.image) </span>

After configuration, click the small triangle icon in front of the audience package to expand and view the sub\-packages.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a2bf73596b64a188ccdd240082846b0~tplv-goo7wpa0wc-image.image) </span>
