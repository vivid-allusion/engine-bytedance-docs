---
title: "Dictionary Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/dictionary-functions"
---

Information regarding connection and configuration of external dictionaries.
<span id="95b3d189"></span>
## dictGetUInt8,dictGetUInt16,dictGetUInt32,dictGetUInt64
<span id="5bc816e6"></span>
## dictGetInt8,dictGetInt16,dictGetInt32,dictGetInt64
<span id="14197958"></span>
## dictGetFloat32,dictGetFloat64
<span id="9c7bc0db"></span>
## dictGetDate,dictGetDateTime
<span id="068ecce6"></span>
## dictgetuid
<span id="4fad0919"></span>
## dictGetString
`dictGetT('dict_name', 'attr_name', id)`

* Use the 'id' key to obtain the value of the attribute 'attr_name' in the dictionary 'dict_name'. `dict_name` and `attr_name` are constant strings. `id` must be UInt64. If the dictionary does not contain the `id` key, then it returns the default specified in the dictionary description.

<span id="db27a912"></span>
## dictGetTOrDefault
`dictGetTOrDefault('dict_name', 'attr_name', id, default)`
Similar to the `dictGetT` function, but the default is taken from the last param of the function.
<span id="aee2977e"></span>
## dictIsIn
`dictIsIn ('dict_name', child_id, ancestor_id)`

* For the 'dict_name' tagged dictionary, check if the 'child_id' key is in (or matches) 'ancestor_id'. Returns UInt8.

<span id="82bb0110"></span>
## dictGetHierarchy
`dictGetHierarchy('dict_name', id)`

* For the 'dict_name' Tag Value Dictionary, returns an array of dictionary keys starting from 'id' and continuing along the parent element chain. Returns Array (UInt64)

<span id="87ef8d7a"></span>
## dictHas
`dictHas('dict_name', id)`

* Check if the dictionary has the specified `id`. If it does not exist, returns 0; if it exists, returns 1.
