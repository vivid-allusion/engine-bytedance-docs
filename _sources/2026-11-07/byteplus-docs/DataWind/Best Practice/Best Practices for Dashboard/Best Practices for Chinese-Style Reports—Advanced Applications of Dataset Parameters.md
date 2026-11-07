---
title: "Best Practices for Chinese-Style Reports—Advanced Applications of Dataset Parameters"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Best_Practices_for_Chinese_Style_Reports_Advanced_Applications_of_Dataset_Parameters"
---

<span id="93828801"></span>
# 1. Overview

Chinese\-style reports are a type of report with unique characteristics and complex requirements. They are typically based on Excel files, processed through a series of steps to generate the final report. This format is an integral part of data management and presentation for most traditional domestic enterprises, and is also referred to as a 'complex report'. The presentation format differs from DataWind dashboards and more closely resembles the style of a pivot table. To meet the diverse and refined management needs of domestic enterprises, Chinese\-style reports usually involve large volumes of data, densely covering numerous detailed and summary data. The calculation methods are complex and varied, including multiple mathematical computations and logical judgments. The statistical dimensions are extensive, requiring comprehensive analysis and presentation of data from multiple perspectives and levels to satisfy the diverse needs of different departments and hierarchies. At the same time, there is a strong emphasis on data completeness and accuracy, striving to present all relevant data precisely and without error. This complexity, combined with selective calculations under specific conditions, means that most agile BI chart functionalities cannot directly and effectively support or display such reports, posing certain challenges for data presentation and analysis.

As shown in the figure below, the format of Chinese\-style reports includes multi\-level summaries and calculations under specific conditions, which existing agile BI or visualization tools cannot easily address through frontend solutions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c21d230453164460b993796ed95ec256~tplv-goo7wpa0wc-image.image) </span>

DataWind supports using custom SQL to pre\-process the required fields, then joining them with the original table to form a new table. The results can then be displayed using the basic pivot table functionality on the frontend, thereby achieving the effect of Chinese\-style reports in DataWind. Additionally, the feature of inserting parameters into direct\-connect datasets can be leveraged, making the final presentation more flexible and superior compared to traditional Excel.

This content cannot be displayed outside of the Lark document at this time.

<span id="49cd9328"></span>
# 2. Steps

By using the custom SQL feature, Chinese\-style reports can be presented in the DataWind dashboard.

<div style="text-align: center">
<strong>Before—result displayed when the original table is not processed</strong></div>


A simple pivot table\-style chart cannot meet the requirements for displaying Chinese\-style reports.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e531ca7c8c09469cb166ad4b903a6911~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<strong>After—result after processing</strong></div>


By leveraging the custom SQL feature, read the original data source, process the required fields, and then join them with the original data to form the desired dataset.

By using the direct connection feature that allows parameters to be passed in, preset parameters can be included in advance, enabling flexibility when displaying charts on the frontend.

<span id="872a985a"></span>
## 2.1 **Connect to data source**

(1) Click **Data Preparation \- Dataset \- Create \- New Dataset \- ClickHouse Data.** 

Note: Since this time we need to use the **insert parameters into direct connection dataset** feature, ClickHouse data must be used.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03f3706e645143c5bc53de27849687cb~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c533a676fddb46afbb391453ea84a6c2~tplv-goo7wpa0wc-image.image) </span>

(2) After adding, go to the following page and select custom SQL and direct connection mode.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccd862cac134471899d3854717a1cb76~tplv-goo7wpa0wc-image.image) </span>

<span id="2c81c69d"></span>
## 2.2 **Build dataset**

According to the actual business scenario, process the fields that require secondary handling using SQL statements, then join them with the original table.

*Application scenario: For example, if the business needs to sum the "sales amount" under certain conditions and there are multiple such scenarios, each field to be summed should be constructed separately and then joined.* 

 **(1) Build a single field**

```Go
 select
      'sum' as `province/autonomous region`,
      'first-level+second-level' as `Shipping Method2`,
      `Order Date`,
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>='2019-01-01'
      and `Order Date`<='2019-06-30'
      and `Shipping Method` in('first-level', 'second-level')
      and `p_date`='2023-09-25'
    group by
      `province/autonomous region`,`Shipping Method2`,`Order Date`
 --Filter out data with Shipping Method as first level or second level, 
 --and group them by province/autonomous region, Shipping Method 2, 
 --and Order Date to sum up the sales amount and quantity--
 --The reason for renaming Shipping Method2 is that the judgment of Shipping Method will be used in the where condition,
 --and not renaming it will cause this judgment to become invalid--  

 --The following format of data will be generated here
 province/autonomous region   Shipping Method2     Order Date       sales amount    quantity
 sum        first-level+second-level     2019-01-01    xxxx     xxxx
 sum        first-level+second-level     2019-01-02    xxxx     xxxx
 ......
 sum        first-level+second-level     2019-06-30    xxxx     xxxx
 --
```


 **(2) Build multiple fields**

Combine the constructed single fields using union all.

```Go
 select
      'sum' as `province/autonomous region`,
      'first-level+second-level' as `Shipping Method2`,
      `Order Date`,
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>='2019-01-01'
      and `Order Date`<='2019-06-30'
      and `Shipping Method` in('first-level', 'second-level')
      and `p_date`='2023-09-25'
    group by
      `province/autonomous region`,`Shipping Method2`,`Order Date`

    union all
  --Splicing the processed fields together using union all, it is important to maintain consistency in the top and bottom structure--  
    select
      'sum' as `province/autonomous region`,
      'second-level+standard-level' as `Shipping Method2`,
      `Order Date`,
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>='2019-01-01'
      and `Order Date`<='2019-06-30'
      and `Shipping Method` in('standard-level', 'second-level')
      and `p_date`='2023-09-25'
    group by
      `province/autonomous region`,`Shipping Method2`,`Order Date`
    union all
   --the same as above--
    select
      'sum' as `province/autonomous region`,
      'first-level+second-level+standard-level' as `Shipping Method2`,
      `Order Date`,
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>='2019-01-01'
      and `Order Date`<='2019-06-30'
      and `Shipping Method` in('first-level', 'second-level', 'standard-level')
      and `p_date`='2023-09-25'
    group by
      `province/autonomous region`,`Shipping Method2`,`Order Date`
      
  --The following format of data will be generated here
 province/autonomous region   Shipping Method2     Order Date       sales amount    quantity
 sum        first-level+second-level     2019-01-01    xxxx     xxxx
 sum        first-level+second-level     2019-01-02    xxxx     xxxx
 ......
 sum        first-level+second-level     2019-06-30    xxxx     xxxx
 sum       second-level+standard-level    2019-01-01    xxxx     xxxx
 ......
 sum       second-level+standard-level    2019-06-30    xxxx     xxxx
 sum    first-level+second-level+standard-level  2019-01-01    xxxx     xxxx
 ......
 sum    first-level+second-level+standard-level  2019-06-30    xxxx     xxxx
 --
```


**Tips:**  Since these need to be displayed under the total, a unified dimension value must be assigned to these fields, and they must be at the same level as provinces. Therefore, a value representing a province or autonomous region can be assigned to these fields.

(3) Join to the original table to form a new table containing all fields required for subsequent chart display.

```Go
select
  `sales amount`,
  `quantity`,
  `province/autonomous region`,
  `Shipping Method2` as `Shipping Method`,
  `Order Date`
  
--It is necessary to change the field names that were previously renamed back here to ensure that the data corresponds to the original table when associated with it--

from
  (
 select
      'sum' as `province/autonomous region`,
      'first-level+second-level' as `Shipping Method2`,
      `Order Date`,
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>='2019-01-01'
      and `Order Date`<='2019-06-30'
      and `Shipping Method` in('first-level', 'second-level')
      and `p_date`='2023-09-25'
    group by
      `province/autonomous region`,`Shipping Method2`,`Order Date`
    union all
    .....
 select
      'sum' as `province/autonomous region`,
      'first-level+second-level' as `Shipping Method2`,
      `Order Date`,
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>='2019-01-01'
      and `Order Date`<='2019-06-30'
      and `Shipping Method` in('first-level', 'second-level','standard-level','当日')
      and `p_date`='2023-09-25'
    group by
      `province/autonomous region`,`Shipping Method2`,`Order Date`
  ) as tmp

union all

select
  `province/autonomous region`,
  `Shipping Method`,
  `Order Date`,
  `sales amount`,
  `quantity`
from
  `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
where
   `Order Date`>='2019-01-01'
  and `Order Date`<='2019-06-30'
  and `p_date`='2023-09-25'
  
  --The following format of data will be generated here
 province/autonomous region   Shipping Method2     Order Date       sales amount    quantity
 sum        first-level+second-level     2019-01-01    xxxx     xxxx
 sum        first-level+second-level     2019-01-02    xxxx     xxxx
 ......
 sum        first-level+second-level     2019-06-30    xxxx     xxxx
 sum       second-level+standard-level    2019-01-01    xxxx     xxxx
 ......
 sum       second-level+standard-level    2019-06-30    xxxx     xxxx
 sum    first-level+second-level+standard-level   2019-01-01    xxxx     xxxx
 ......
 sum    first-level+second-level+standard-level   2019-06-30    xxxx     xxxx
 Shanghai            first-level      2019-01-01    xxxx     xxxx
 Shanghai            first-level      2019-01-03    xxxx     xxxx
 Beijing            first-level      2019-01-05    xxxx     xxxx
 ......
 --
```


<span id="aadfc08e"></span>
## 2.3 Create visualizations

To perform visual queries on the dataset generated by the previous operations, only a few adjustments to the tables are needed to achieve the style of traditional Chinese reports. This enables the basic display of Chinese\-style reports in DataWind.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70aab7a528234a6c90da4c34f595d7aa~tplv-goo7wpa0wc-image.image) </span>

<span id="57e6d2a8"></span>
# 3.**Add parameters to increase report flexibility**

After implementing the basic Chinese\-style report, parameters can be used to add greater flexibility to the charts.

<span id="1e8481c0"></span>
## 3.1 Configure parameters

Configure the required parameters in advance to facilitate subsequent use. Click **Data Preparation \- Dataset \- Parameter Management \- Create Parameter,**  to create the necessary public parameters.

*Use case: By switching dates and different provinces, you can display the required data segments. Therefore, it is necessary to establish relevant date parameters and a province parameter (see the figure below).* 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/837752404c944463baaf85bc98b4e532~tplv-goo7wpa0wc-image.image) </span>

Considering scenarios where multiple provinces may be selected, a multi\-select logic is used. The date parameter is relatively conventional and just set a default value.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/321a358369374a929388beab6c1cd477~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83ae1f680123428491d04752f14beb3e~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**Tips:**  For multi\-select and single\-select parameter logic, whether writing in SQL or adding fields in DataWind, there are some differences in syntax:


* If single\-select, use '=' for comparison (single\-select may also use 'in' for comparison):


``Province/Autonomous Region`= {Province/Autonomous Region}`


* If the parameter is multi\-select, use 'in' logic when writing the condition **and do not forget the parentheses**:


``Province/Autonomous Region`in ({Province/Autonomous Region})`

<span id="0a224cae"></span>
## 3.2 Insert parameters

In the ClickHouse data source, click **Insert Parameter** in custom SQL under direct connection, and insert the required parameter placeholder at the corresponding position.

**Parameter construction:** 

 **(1) Single field construction**

```Go
select
      'sum' as `province/autonomous region2`,
      'first-level+second-level' as `Shipping Method2`,
      `Order Date`,
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>={start date}
      and `Order Date`<={end date}
      
      --Here, two date parameters are introduced as future conditional judgments, such as
      start date为2019-01-01 end date为2019-06-30
      --The actual conditions here are:
      `Order Date`>='2019-01-01'
      and `Order Date`<='2019-06-30' 
      --Consistent with the previous logic--
      
      and `Shipping Method` in ('first-level', 'second-level')
      and `p_date`='2023-09-25'
      and `province/autonomous region` in ({province/autonomous region})
      
      --Another parameter has been introduced here{province/autonomous region}
      --But since the parameter{province/autonomous region} is a multiple-choice value,
      --such as selecting Shanghai and Beijing,
      --here is `province/autonomous region` in ('Shanghai','Beijing'),
      --So we need to use 'in' to make a judgment,
      --not`province/autonomous region` = {province/autonomous region} to make a judgment--  
      
    group by
      `province/autonomous region2`,`Shipping Method2`,`Order Date`
```


 **(2) Multiple field construction**

```Go
select
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`,
      'sum' as `province/autonomous region2`,
      'first-level+second-level' as `Shipping Method2`,
      `Order Date`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>={start date}
      and `Order Date`<={end date}
      and `Shipping Method` in('first-level', 'second-level')
      and `p_date`='2023-09-25'
      and `province/autonomous region` in ({province/autonomous region})
    group by
      `province/autonomous region2`,
      `Shipping Method2`,
      `Order Date`
    union all
        --The logic here is the same as above,
    --using union all to concatenate content with the same table structure,
    --involving multiple fields that can be pieced together in this way--
    select
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`,
      'sum' as `province/autonomous region2`,
      'second-level+standard-level' as `Shipping Method2`,
      `Order Date`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>={start date}
      and `Order Date`<={end date}
      and `Shipping Method` in('standard-level', 'second-level')
      and `p_date`='2023-09-25'
      and `province/autonomous region` in ({province/autonomous region})
    group by
      `province/autonomous region2`,
      `Shipping Method2`,
      `Order Date`
```


 **(3) Combine the newly constructed fields with the original table to generate a new dataset**

```Go
select
  `sales amount`,
  `quantity`,
  `province/autonomous region2` as `province of affiliation`,
  `Shipping Method2` as `order channel`,
  `Order Date`
from
  (
    select
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`,
      'sum' as `province/autonomous region2`,
      'first-level+second-level' as `Shipping Method2`,
      `Order Date`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>={start date}
      and `Order Date`<={end date}
      and `Shipping Method` in('first-level', 'second-level')
      and `p_date`='2023-09-25'
        and `province/autonomous region` in ({province/autonomous region})
    group by
      `province/autonomous region`,
      `Shipping Method2`,
      `Order Date`
    union all
    .....
    --Here are all the fields that need to be constructed--
    union all
    select
      sum(`sales amount`) as `sales amount`,
      sum(`quantity`) as `quantity`,
      'sum' as `province/autonomous region2`,
      'All Method' as `Shipping Method2`,
      `Order Date`
    from
      `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
    where
      `Order Date`>={start date}
      and `Order Date`<={end date}
      and `Shipping Method` in('first-level', 'second-level', 'standard-level', '当日')
      and `p_date`='2023-09-25'
        and `province/autonomous region` in ({province/autonomous region})
    group by
      `province/autonomous region`,
      `Shipping Method2`,
      `Order Date`
  ) as tmp
union all
select
  `sales amount`,
  `quantity`,
  `province/autonomous region` as `province of affiliation`,
  `Shipping Method` as `order channel`,
  `Order Date`
--When splicing, it is important to note that the structure names of the two tables need to be consistent--
from
  `aeolus_data_db_rangers_202309`.`aeolus_data_table_22_3751_prod`
where
  `Order Date`>={start date}
  and `Order Date`<={end date}
  and `p_date`='2023-09-25'
  and `province/autonomous region` in ({province/autonomous region})
```


After inserting parameters, in the SQL for constructing table values, the statistical results for different parameter conditions will be automatically calculated based on the selected parameter  **{Province/Autonomous Region}**   **.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc59e23d1b7c43b2a109ee45813bbb80~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69241e724e2f4706a4379cacf141ffe9~tplv-goo7wpa0wc-image.image) </span>

<span id="4494f6c0"></span>
## 3.3 **Dashboard filter adjustment**

By adding parameters to the dashboard, adjusting parameter visibility, associating parameters with filters, changing the order of filter conditions, and other methods, the frontend display can be optimized, thereby achieving a more flexible presentation of Chinese\-style reports on DataWind.
