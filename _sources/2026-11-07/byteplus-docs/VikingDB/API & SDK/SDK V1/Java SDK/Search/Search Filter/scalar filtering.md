---
title: "scalar filtering"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/javasdk_scalar_filtering"
---

You can filter results in a vector database using a scalar filter.

Scalar filtering is a feature that allows you to refine vector search results by applying conditions to scalar fields. This reference guide explains how to use the Filter parameter, details the available query operators (such as must, range, and, or), and provides a complete Java SDK code example to demonstrate implementation. Use this guide to construct precise, multi\-conditional queries in your vector database.

<span id="5d1ccdb9"></span>
# Parameter description


|**parameter** |**type** |**Is it required?**  |**default value** |**parameter description** |
|---|---|---|---|---|
|Filter |Map |No |None |For details on filter conditions, see the **Filter expression section.** <br><br><br>* Default is empty, no filtering.<br><br>* Filter conditions include four query operators (must, must_not, range, and range_out) and two combination operators (and and or).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The precondition for a filter is that the corresponding field has a scalar index enabled.</div><br> |


<span id="fe6208d4"></span>
# Filter expression


|**operator** |**operator description** |**example** |
|---|---|---|
|Must |Applies to the specified field. This means the value must be in the list [...]. |```JSON```<br>```{```<br>```  "op": "must",```<br>```  "field": "region",```<br>```  "conds": ["cn", "sg"]```<br>```}```<br> |
|must_not |Applies to the specified field. This means the value must not be in the list [...]. |```JSON```<br>```{```<br>```  "op": "must_not",```<br>```  "field": "data_type",```<br>```  "conds": [1,2,3]```<br>```}```<br> |
|Range |Applies to the specified field, meaning the value must be within the specified range.<br><br>Use `gte (greater than or equal to), gt (greater than), lte (less than or equal to), and lt (less than) to define a one-dimensional range.`<br><br>`In addition, you can use center and radius to represent a circular range in two dimensions.` |```JSON```<br>```// The price is in the range [100.0, 500.0).```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0,```<br>```  "lt": 500.0```<br>```}```<br>``````<br>```//price >= 100.0```<br>```{```<br>```  "op": "range",```<br>```  "field": "price",```<br>```  "gte": 100.0```<br>```}```<br>``````<br>```// Within a circle with the specified center and a radius of 50.0.```<br>```{```<br>```  "op": "range",```<br>```  "field": ["pos_x", "pos_y"],```<br>```  "center": [100.0, 123.4],```<br>```  "radius": 50.0```<br>```}```<br> |
|range_out |Applies to the specified field, meaning the value must be outside the specified range. Use `gte (greater than or equal to), gt (greater than), lte (less than or equal to), and lt (less than) to define a one-dimensional range.` |```JSON```<br>```// Filters for items with a price less than 100.0 or greater than 500.0.```<br>```{```<br>```  "op": "range_out",```<br>```  "field": "price",```<br>```  "gt": 500.0,```<br>```  "lt": 100.0```<br>```}```<br> |
|And |A logical operator that returns the intersection of multiple conditions. |```JSON```<br>```{```<br>```  "op": "and",   // Operator name```<br>```  "conds": [     // A list of conditions. Supports nested logical operators and must/must_not operators.```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...         // Supports combining one or more conditions.```<br>```    }```<br>```  ]```<br>```}```<br> |
|Or |A logical operator that returns the union of multiple conditions. |```JSON```<br>```{```<br>```  "op": "or",   // Operator name```<br>```  "conds": [    // A list of conditions. Supports nested logical operators and must/must_not operators.```<br>```    {```<br>```      "op": "must",```<br>```      "field": "type",```<br>```      "conds": [1]```<br>```    },```<br>```    {```<br>```        ...      // Supports combining one or more conditions.```<br>```    }```<br>```  ]```<br>```}```<br> |


<span id="4b0f4b4d"></span>
# Example

```Java
// Call the related operation once during the initialization of the program to get the specified index. 
Index index = vikingDBService.getIndex("javaSDKTest", "test_index");
```


```Java
// Define the output fields list, which fields will be returned in the search results
List<String> outputFields = Arrays.asList("f_id", "city", "employee_name", "age");

// Create a condition list to store multiple query conditions
List<Map<String, Object>> conditionsList = new ArrayList<>();

// Condition 1: The country must be "China".
Map<String, Object> condition1 = new HashMap<>();
condition1.put("op", "must"); // Operator, indicating "must" be satisfied
condition1.put("field", "country"); // Field name
condition1.put("conds", Arrays.asList("China")); // Condition value
conditionsList.add(condition1); // Add the condition to the condition list

// Condition 2: The city must be "Chengdu".
Map<String, Object> condition2 = new HashMap<>();
condition2.put("op", "must"); // Operator, indicating "must" be satisfied
condition2.put("field", "city"); // Field name
condition2.put("conds", Arrays.asList("Chengdu")); // Condition value
conditionsList.add(condition2); // Add the condition to the condition list

// Condition 3: Age must be greater than 25
Map<String, Object> condition3 = new HashMap<>();
condition3.put("op", "range"); // Operator, indicating range query
condition3.put("field", "age"); // Field name
condition3.put("gt", 25); // Greater than 25 years old
conditionsList.add(condition3); // Add the condition to the condition list

// Create a filter to combine all conditions
Map<String, Object> filter = new HashMap<>();
filter.put("op", "and"); // Use the logical "AND" operator to connect all conditions
filter.put("conds", conditionsList); // Set the condition list as the content of the filter

// Print the filter content for debugging purposes
System.out.println("Filter: " + filter);

// Execute the search operation
List<Object> searchResults = index.search(new SearchParam()
                .setScalarOrder(new ScalarOrder("age", "asc").build()) // Sort by age in ascending order
                .setOutputFields(outputFields) // Set the fields to be returned
                .setFilter(filter) // Set the filter conditions
                .setLimit(20) // Limit the number of returned results to 20
                .build()); // Build the search parameters

// Print the search results
System.out.println("Search Results: " + searchResults);
```


<span id="170e9970"></span>
## Return value

The Java call for this task returns a `List. The properties contained in the DataObject instance are shown in the following table.`


|**attribute** |**explain** |
|---|---|
|ID |The primary key ID. |
|Fields |A map containing the data for the fields returned in the request. |
|Score |Indicates the degree to which the found vector matches the input vector. |
