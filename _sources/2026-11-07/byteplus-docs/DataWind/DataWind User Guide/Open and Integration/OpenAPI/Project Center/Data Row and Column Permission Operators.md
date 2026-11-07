---
title: "Data Row and Column Permission Operators"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Data_Row_and_Column_Permission_Operators"
---


| |op |valOption |val |
|---|---|---|---|
|String data type | | | |
|Contains |"like" | |["234", "34234", "23423"] |
|Does not contain |"not like" | |["123", "234"] |
|Starts with |"like" | |["123", "234"] |
|Ends with |"like" | |["123", "234"] |
|Numeric data type | | | |
|Greater than |"\>" |{} |[1] |
|Greater than or equal to |"\>=" |{} |[1] |
|Less than |"<" |{} |[1] |
|Less than or equal to |"<=" |{} |[1] |
|Range |"between" | |[1, 3] |
|Range |"between" | |[1, 3] |
|Range |"between" | |[1, 3] |
|Range |"between" | |[1, 3] |
|Is null |"is null" |{} |[null] |
|Is not null |"is not null" |{} |[null] |
|Type like 'array<%\>' | | | |
|ArrayHas |"arrayHas" |{} |["1", "2"] |
|NotArrayHas |"notArrayHas" |{} |["1", "2"] |
|Date and datetime data types | | | |
|Range |"between" |{} |date：["2021\-08\-25", "2021\-08\-25"]<br><br>datetime：["2021\-08\-25 00:00:00", "2021\-08\-25 23:59:59"] |
|> = |"advancedDate" |{"endTime": {"type": "unlimited"},<br><br>"startTime": {<br><br>"type": "fixed",<br><br>"val": "2021\-08\-18"}<br><br>} |[null] |
|<= |"advancedDate" |{<br><br>endTime: {type: "fixed", val: "2021\-08\-25"},<br><br>startTime: {type: "unlimited"}<br><br>}{} |[null] |
