---
title: "Date"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/date"
---

Date type, stored in two bytes, indicating the date value from 1970-01-01 (unsigned) To the current date. Allows storage from the Unix Start epoch To a defined cap threshold constant at the compile stage (the current cap is 2106, But the ultimately fully Supported year is 2105). The minimum output is 1970-01-01.
Value Scope: [1970-01-01, 2149-06-06].
No Timezone information is stored in the Date.
