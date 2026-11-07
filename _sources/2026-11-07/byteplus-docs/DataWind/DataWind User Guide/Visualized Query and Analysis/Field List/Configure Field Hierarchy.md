---
title: "Configure Field Hierarchy"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Configure_Field_Hierarchy"
---

This product only supports configuring hierarchies for dimension fields. For dimension fields with hierarchical relationships, such as country\-province\-city or an enterprise's organizational hierarchy, it is necessary to configure the hierarchy to enable data [Drill Up and Drill Down](https://docs.byteplus.com/docs/DataWind/Drill_Up_and_Drill_Down). This article describes how to create, add, adjust, remove, rename, and delete hierarchies.

<span id="2ff3a115"></span>
# Prerequisites

Your account must have dataset editing permissions to **create and adjust hierarchies**. For authorization operations, see [Role Management](https://docs.byteplus.com/docs/DataWind/Role_Management) **.** 

<span id="_2-功能介绍"></span>
# Create and add hierarchies

<span id="27f1da2f"></span>
## Create a hierarchy


1. The data fields are as shown below: province, city, and district/county.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f95f85d841b4189965553c58e6decaf~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

2. To set up a province\-city\-district/county hierarchy, click to the right of "province" and select "Create hierarchy." You can name this hierarchy structure.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66f732c49229447382d2f07d33e021c6~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. After confirming, the newly added hierarchy structure and its fields will be visible in the dataset list.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c5470dd0c96477185763c57c120acbe~tplv-goo7wpa0wc-image.image" width="562px" />   </div>
   


<span id="9a87e5a5"></span>
## Add to hierarchy


1. To add the city and district/county fields to this hierarchy, select the city and district/county fields and choose "Add to hierarchy."

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24c244d999404422864ae0a433df1ac2~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

2. Then select the target hierarchy name.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2dbf27ad8b1c4fb0af15bf1b44ba5261~tplv-goo7wpa0wc-image.image" width="628px" />   </div>
   

3. The target hierarchy structure will be created.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c003e9e514634a7c9c0f11e06bc3a0c7~tplv-goo7wpa0wc-image.image" width="660px" />   </div>
   


<span id="13a69780"></span>
# Modify or delete hierarchies

<span id="_2-3-调整层级结构"></span>
## Adjust the hierarchy structure

The order of fields within a hierarchy can be changed by dragging and dropping them within the hierarchy structure.

<span id="_2-4-移出层级"></span>
## Remove from hierarchy

The reverse operation of adding to a hierarchy: if a field in the hierarchy structure does not belong to the target hierarchy, you can choose to remove it from the hierarchy.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8871563a22644daf95bc69bc055d439b~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-5-重命名层级名称"></span>
## Rename a hierarchy

To modify a previously set hierarchy name, use this function.

Click the right side of the hierarchy structure and select "Rename" to rename the hierarchy structure.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c1f1ecadbc942e1bc4d93ee31b48f9d~tplv-goo7wpa0wc-image.image" width="724px" /></div>


<span id="_2-6-删除层级"></span>
## Delete a hierarchy

If the hierarchy structure is no longer needed, select the hierarchy information and choose "Delete."

Caution: Deleting a hierarchy will not affect the fields within the hierarchy structure; only the hierarchy structure information will be deleted.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22f0e1cda6224559b8bd7f1ce74cf0bb~tplv-goo7wpa0wc-image.image" width="704px" /></div>
