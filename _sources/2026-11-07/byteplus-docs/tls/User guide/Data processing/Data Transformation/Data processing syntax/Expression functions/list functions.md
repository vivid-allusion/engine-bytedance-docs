---
title: "list functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/list_functions"
---

This document describes the syntax and typical examples of list functions.

<span id="e78a7431"></span>
## lst_make

lst_make function is used to create a list.

<span id="460c9277"></span>
### Function syntax and format

```Python
lst_make(values...)
```


Parameters are described as follows:


|Parameter |Type |Required |Description |
|---|---|---|---|
|values |String |Yes |The elements of the list.<br><br>You can add one or more elements. |


<span id="cf25b3dd"></span>
### Sample function

Create a string list containing strings a and b.


* Transformation rule:

   ```Python
   f_set("list",lst_make("a","b")
   ```
   

* Log:

   ```JSON
   {}
   ```
   

* Transformation result:

   ```Plain
   {
       "list": [
         "a",
         "b"
          ]
   }
   ```
   


<span id="275ae982"></span>
## lst_append

lst_append function is used to append elements to the end of the list.

<span id="eb9284d0"></span>
### Function syntax and format

```Python
lst_append(list,values...)
```


Parameters are described as follows:


|Parameter |Type |Required |Description |
|---|---|---|---|
|list |List |Yes |The list of elements to be appended. |
|values |String |Yes |The elements that you want to append.<br><br>You can add one or more elements. |


<span id="cd477838"></span>
### Sample function

Append element c to the list.


* Transformation rule:

   ```Python
   f_set("list_new",lst_append(v('list'),"c")
   ```
   

* Log:

   ```JSON
   {
       "list": [
         "a",
         "b"
          ]
   }
   ```
   

* Transformation result:

   ```Plain
   {
       "list": [
         "a",
         "b"
          ],
       "list_new": [
         "a",
         "b"，
         "c"
          ]
   }
   ```
   


<span id="3bb6c1b6"></span>
## lst_delete_at

lst_delete_at function is used to delete elements at the specified position in the list.

<span id="38b921f8"></span>
### Function syntax and format

```Python
lst_delete_at(list,index)
```


Parameters are described as follows:


|Parameter |Type |Required |Description |
|---|---|---|---|
|list |List |Yes |The list of elements to be deleted. |
|index |Int |Yes |The position of the element that you want to delete. The position of the first element is 0. |


<span id="a832e869"></span>
### Sample function

Deleted the first element in the list.


* Transformation rule:

   ```Python
   f_set("list_new",lst_delete_at(v('list'),0)
   ```
   

* Log:

   ```JSON
   {
       "list": [
         "a",
         "b"
          ]
   }
   ```
   

* Transformation result:

   ```Plain
   {
       "list": [
         "b"
          ]
   }
   ```
