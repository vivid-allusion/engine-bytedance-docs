---
title: "Fields and Field Expressions FAQs"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Fields_and_Field_Expressions_FAQs"
---

<span id="_1-数据源字段与数据集字段"></span>
# 1. Data source fields and dataset fields

Background: When using the "Add field" feature, users will notice that the field list on the left contains two types. One is data source fields, and the other is dataset fields. So what is the difference between these two types? Which type of field should users select when writing expressions?

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/693855ec6c164ee28479cedd0a73c917~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-1-什么是数据源字段？"></span>
## 1.1 What are data source fields?

As the name suggests, data source fields are fields that originate from the data source. For example, in the dataset shown below, the data source is Feishu Sheets, and the fields contained within Feishu Sheets itself are data source fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/381d8a86a53040faa8525cefe824f743~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-2-什么是数据集字段？"></span>
## 1.2 What are dataset fields?

Dataset fields are the fields contained within the dataset. These fields are not the fields from the data source itself, but are fields automatically created by the dataset, as well as fields newly created by users using expressions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d88e0b1f77e41c4813281e49dbed14f~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-3-数据源字段与数据集字段有什么区别？"></span>
## 1.3 What is the difference between data source fields and dataset fields?

Data source fields cannot be queried directly. On the left side of the visual query page, the field list displayed consists entirely of dataset fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35de206a42e64e6e975c055097eb49e7~tplv-goo7wpa0wc-image.image) </span>

After the dataset's data source is parsed, the dataset will automatically generate a dataset field for each data source field on the field configuration page. The expression for each of these initial dataset fields is the corresponding data source field itself.

For example, in the dataset field "Payment type" shown below, its expression is the 'Payment type' data source field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcdaea5489a14f9db55209879b41a03c~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-4-同名的数据源字段和数据集字段有什么区别？"></span>
## 1.4 What is the difference between data source fields and dataset fields with the same name?

The result represented by a data source field is the original result from the data source, whereas a dataset field must follow its specific expression.

The following example helps illustrate this:

When the expression of a dataset field is the same as that of a data source field, then at this point, there is no difference between the dataset field and the data source field. For example, in the figure below, the dataset field "order_date" uses the expression 'order_date', which is the corresponding data source field. Therefore, the results of both are identical.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d30a19a98e6e48e1862fc1cf56940c64~tplv-goo7wpa0wc-image.image) </span>

Since the expression of a dataset field can be freely modified, some dataset field expressions may be changed later, resulting in expressions that are no longer the same as their original corresponding data source fields.

For example, in the figure below, the "product_type" field may have originally used the expression `product_type`, but it has now been changed to count(`product_type`). At this point, the meanings represented by these two fields are completely different. To use the original meaning of "product_type", the data source field must be selected.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb1476174ffc451387a62390a560b0ce~tplv-goo7wpa0wc-image.image) </span>

As for fields newly created by users, since there are no corresponding data source fields, this issue does not need to be considered.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bf7082e940744d088dc8311fd873336~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-公共字段与个人字段"></span>
# 2. Public fields and personal fields

Background: There are two main types of fields in a dataset: dataset fields and personal fields. Dataset fields can also be referred to as public fields.

<span id="_2-1-什么是公共字段，什么是个人字段？"></span>
## 2.1 What are public fields and what are personal fields?

Public fields are fields within the dataset that are directly added to the dataset. Every authorized user can view and use these fields. For example, the fields visible to all users in the figure below are public fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4999a8ab27764eb29afdc681211ae9d1~tplv-goo7wpa0wc-image.image) </span>

Public fields are fields belonging to the dataset itself. Adding a public field is equivalent to modifying the dataset, so only users with dataset editing permissions can add public fields.

Because the content of a dataset cannot be easily modified, dataset editing permission is a relatively high\-level permission, held by only a few users.

However, when users are working with this dataset and want to add fields, they can add personal fields. Personal fields do not affect the functionality of the dataset itself.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/230ce880954645bdb66d5fc9502ba30d~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-如何选择添加公共字段或个人字段？"></span>
## 2.2 How to choose to add a public field or a personal field?

When adding a field, there is an option in the lower left corner labeled "Save to dataset." If this option is selected, the field will be saved to the dataset and become a dataset field, that is, a public field.

If it is not selected, a personal field will be created.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Creating a public field involves modifying the dataset, so only users with dataset editing permissions can select the "Save to dataset" option. Users with only the following editing permissions can only create personal fields.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8828ca742174d5888f85c501098840f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-个人字段有什么特点以及怎么区分？"></span>
## 2.3 What are the characteristics of personal fields and how to distinguish them?

(1) Carefully observe the diagram below: "order_date" is a public field, while "province_sale" is a personal field. When personal fields appear in the field list or are placed in the field bar, the font is italicized. Additionally, in the field bar, the font color is blue.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18421d8b0ed84e2d9b628483fe7fc85f~tplv-goo7wpa0wc-image.image) </span>

(2) When adding fields, both public fields and personal fields can be referenced. However, when a personal field is referenced, it is prefixed with [private] to indicate that it is a personal field. For example, in the diagram below, the first row is a public field, and the second row is a personal field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/deeac2392163418b95c5f4c5093d4bcf~tplv-goo7wpa0wc-image.image) </span>

(3) Personal fields are only displayed in the creator's field list and cannot be searched by other users.

However, DataWind supports sharing query links with other users. If a personal field is used in the current user's query and then shared with other users, what impact does this have?

Refer to the diagram below: other users can view the current user's personal fields in the chart. However, in the field bar, the font color of personal fields is gray, and the font is italicized. Other users do not have permission to search for the current user's personal fields, but they can drag the corresponding field from the dimension section to the metric section and similar operations.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4034d16d0d751071eb1c8325fb23ce75.png) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If, after clicking the share link, the user finds that a field is grayed out, it is not necessarily another user's personal field. When a field is a dataset field but has been deleted from the dataset, its font color will also appear gray in the query link. How to determine whether this field is a personal field or a deleted field? Refer to the figure below: italicized text indicates a personal field, while non\-italicized text indicates a deleted field.</div>


<span id="_2-4-为什么直接复制其他用户的表达式创建字段会报错？"></span>
## 2.4 Why does directly copying another user's expression to create a field result in an error?

Personal fields can only be referenced by their creators. If an expression references another user's personal field, directly using this expression to create a field will result in an error.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/deeac2392163418b95c5f4c5093d4bcf~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-怎么查看其他用户的个人字段的表达式？"></span>
## 2.5 How to view the expression of another user's personal field?

Users with edit permissions for the dataset can view, and can only view, other users' personal fields that have been placed in a chart. Users can click the downward triangle in front of the field bar and select "Edit field" from the expanded options to view the expression of this field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fbacb5aa1444d1cbf1c85f45362e8d3~tplv-goo7wpa0wc-image.image) </span>

If the current personal field is in the filter bar and there is no "Edit field" option, drag the current field to the dimension or metric bar, then select "Edit field" to view it.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the expression of this personal field references other personal fields, it is not possible to further view the referenced personal fields.</div>


<span id="_2-6-总结"></span>
## 2.6 Summary


|**Question** |**Public field** |**Personal field** |
|---|---|---|
|Concept |Fields that belong to the dataset itself, or fields added to the dataset by users |Fields created by users themselves, not added to the dataset |
|How to create |Select Save to Dataset or add to the dataset |Do not select Save to Dataset |
|Permissions required for creation or modification |Dataset edit and higher permissions |Dataset view and lower permissions |
|Who can use or search for it? |All users with dataset permissions |Field creator |
|Is there any difference in usage? |No |No |
|Can it be referenced by other field expressions? |Yes |Yes (public field expressions cannot reference personal fields) |
|How can the current user distinguish whether it is a personal field? |Non\-italic font |Italic font, blue font in the field bar, and the tooltip will display "Personal Field" |
|How can other users distinguish between personal fields and deleted fields? |Non\-italic font |Italic font |


<span id="_3-其他常见问题"></span>
# 3. Other frequently asked questions

<span id="_3-1-什么是字段表达式？"></span>
## 3.1 What is a field expression?

A field expression mainly consists of fields and functions, and may also include constants or parameters. To reference other fields, the referenced field must be searchable in the field list on the left. Some commonly used functions are also provided on the right.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efe871e81c1b4459bda26563e2c423fb~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-维度和指标有什么区别？"></span>
## 3.2 What is the difference between dimensions and metrics?

There is no clear boundary between dimensions and metrics. For example, in a class score dataset, to view each student's score in the class, the student name is the dimension and the score is the metric. To view the number of students in each score range, the score is the dimension and the count of names is the metric.

<span id="_3-3-为什么有的字段不能被拖到维度？"></span>
## 3.3 Why can some fields not be dragged to dimensions?

Check whether the current field is an aggregation field. Aggregation fields cannot be used as dimensions.

<span id="_3-4-什么是聚合字段？"></span>
## 3.4 What is an aggregation field?

Simply put, if a field's expression contains an aggregation function or references another aggregation field, then this field is an aggregation field.

<span id="_3-5-什么是聚合函数？"></span>
## 3.5 What is an aggregation function?

Aggregation means combining multiple data items into a whole through certain calculation methods. For example, the most common sum function. The purpose of sum is to calculate the total of a set of data and produce a single value, which is essentially an aggregation process. Other functions such as count, avg, max, min, quantile, and groupArray are also aggregate functions. When these functions are used in the expression of a field, that field is considered an aggregate field.

<span id="_3-6-如何识别一个字段是否为聚合字段？"></span>
## 3.6 How to identify whether a field is an aggregate field?

In addition to determining this through the expression, you can also place the field in the metrics section. If the metrics capsule displays "Aggregate" in front of the field, it is an aggregate field; otherwise, it is a non\-aggregate field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5828b6e5db7b47de91845e2fb848e0a7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-7-非聚合字段放在指标栏前面显示的「求和」是什么意思？"></span>
## 3.7 What does "Sum" mean when it appears in front of a non\-aggregate field in the metrics section?

Except for detail tables, other charts will automatically apply an aggregation method to non\-aggregate fields during queries. For example, the fields shown in the figure below will be automatically aggregated when queried. For numeric types, the default aggregation method is sum, and the value displayed in the chart is the result of summing this field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6b49faa9209415ba81af8083108c82f~tplv-goo7wpa0wc-image.image) </span>

Users can click the downward triangle in front of the metric to select other aggregation methods.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a4355ac91064abc97dbebaa6616d634~tplv-goo7wpa0wc-image.image) </span>

For aggregate fields, since they have already been aggregated, the metrics capsule will display "Aggregate" in front of the field, and no other aggregation methods can be selected.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c1b3f6ed9c34cacb41cc4e9b39a396a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-8-可以把聚合字段放在维度中吗？"></span>
## 3.8 Can aggregate fields be placed in dimensions?

When an aggregate function is used in a hierarchical field (used as a dimension), the LOD function can be used. The LOD function can calculate results aggregated by specified dimensions. Importantly, although aggregation is used within the LOD function, its calculation result is not an aggregate field.

For a detailed introduction to the LOD function, see [LOD Expression](https://docs.byteplus.com/docs/DataWind/LOD_Expression).

Example: To categorize provinces based on the total payment amount for each province, provinces with totals greater than or equal to 100,000,000 are classified as level one, those less than 100,000,000 but greater than or equal to 10,000,000 as level two, and others as level three. Finally, the goal is to count the number of provinces in each category.

Generally, users may calculate this using the expression shown in the figure below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ea655e817c041eb89bcb88e1ee9d41a~tplv-goo7wpa0wc-image.image) </span>

However, this field can only be placed in metrics, not in dimensions. This is because the expression uses an aggregation function, making it an aggregated field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccdefc31d22f4f67b2337c15bbfb2eec~tplv-goo7wpa0wc-image.image) </span>

At this point, you can replace `sum('sale_price')` with an LOD function: `{filter=true:fixed [province]:sum(sale_price)}`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cbcddbafd094f54abd7334bb628b860~tplv-goo7wpa0wc-image.image) </span>

This way, the created field can be placed in dimensions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d43a19e0a642412a85c2f7961f118167~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-9-字段的口径问题-字段的数据跟线上对不上应该问谁？"></span>
## 3.9 Field granularity issues & whom to ask if field data does not match the online data?

**Background:**  The DataWind platform does not know what data is stored in the user's dataset, nor does it know the granularity of each field. Only the dataset administrator understands these issues.

If a user encounters similar issues while viewing a dashboard, they can consult the dashboard owner.

If a user encounters similar issues during a visualization query, they can first consult the owner of the dataset currently being queried.
