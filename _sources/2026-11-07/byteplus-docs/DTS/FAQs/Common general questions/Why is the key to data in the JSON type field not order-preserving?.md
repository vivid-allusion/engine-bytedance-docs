---
title: "Why is the key to data in the JSON type field not order-preserving?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/why_is_the_key_to_data_in_"
---

Because in JSON format, name\-value pairs are accessed by name, not by order. However, the elements of a JSON array are ordered and can be accessed by indices. Therefore, in a JSON object, the order of the keys is not guaranteed, while the values in the array are ordered. This design ensures the flexibility and consistency of JSON, while avoiding potential problems caused by field order. For more information about JSON, refer to [The JSON Data Type](https://dev.mysql.com/doc/refman/8.4/en/json.html).
