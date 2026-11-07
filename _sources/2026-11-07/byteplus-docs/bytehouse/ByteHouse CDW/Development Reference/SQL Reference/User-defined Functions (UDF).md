---
title: "User-defined Functions (UDF)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-user-defined-functions-udf"
---

ByteHouse Cloud Data Warehouse version supports User\-defined Functions (UDF), which can process data by calling any external executable program or script.

ByteHouse cloud data warehouse version supports the following types of UDF:


1. Lambda UDF: User\-defined Lambda function.

2. Python UDF: Functions defined in Python language and return results (Beta function, currently only supported in Beijing v1 cluster).


<span id="a55563ae"></span>
## Lambda UDF

Users can create custom functions using a Lambda expression. This expression must be composed of function parameters, constants, operators, or other function calls.

<span id="1535e507"></span>
### **Syntax**

```SQL
CREATE FUNCTION name AS (parameter0, ...) -> expression
```


<span id="85c9d214"></span>
### **Restrictions**

There are no restrictions on the number of parameters for functions.

Conditions:


* The function name must be unique and must not duplicate existing user\-defined or system function names.

* Recursive functions are not allowed.

* All variables used in the function must be specified in its parameter list.


If a UDF does not meet any of the above restrictions, it may cause exceptions.

<span id="7e3af558"></span>
### Prerequisites

When creating and using a UDF, you must first create and specify a database.

```SQL
CREATE DATABASE myudf;
USE myudf;
```


<span id="3f463eda"></span>
### Usage Example

Example 1:

```SQL
CREATE FUNCTION linear_equation AS (x, k, b) -> k*x + b;
SELECT number, linear_equation(number, 2, 1) FROM numbers(3); 
```


As a result 1:

```Plain
┌─number─┬─plus(multiply(2, number), 1)─┐
│      0 │                            1 │
│      1 │                            3 │
│      2 │                            5 │
└────────┴──────────────────────────────┘
```


Example 2:

In the following query, the conditional function if is called within a user\-defined function:

```SQL
CREATE FUNCTION parity_str AS (n) -> if(n % 2, 'odd', 'even');
SELECT number, parity_str(number) FROM numbers(3); 
```


As a result 2:

```Plain
┌─number─┬─if(modulo(number, 2), 'odd', 'even')─┐
│      0 │ even                                 │
│      1 │ odd                                  │
│      2 │ even                                 │
└────────┴──────────────────────────────────────┘
```


<span id="72283b0f"></span>
## Python UDF

Python UDF is a Python script called via ByteHouse. Python UDF contains a Python program that runs and returns a single value when a function is called.

When a query calls a Python UDF, the following steps occur:


1. The function converts input parameters into Python Numpy Data type.

2. The function passes the converted input parameters and then runs the Python program.

3. Python code returns a single value. The data type of the return value must correspond to the specified RETURNS data type in the function definition.

4. The function converts the return value from Python to the defined data type, then returns that value to the query.


<span id="3ddbaacb"></span>
### Usage restrictions


* The Python UDF functionality is a Beta feature. Please contact the ByteHouse Product Manager to request whitelist access.

* Ensure that your ByteHouse engine version is v2.3.x and higher. You can log in to the ByteHouse Cloud Data Warehouse Console, click the **Tenant management** at the top, and view your engine version on the **Basic information** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48e6361f21d64da3b4c1276d1a5f98c3~tplv-goo7wpa0wc-image.image) </span>

* Currently, only Python 3.9 is supported.


<span id="ce417ea8"></span>
### Data type


|**SQL Type** |**Python Type** |**Remark** |
|---|---|---|
|UInt8 |NPY_UINT8 |None |
|UInt16 |NPY_UINT16 |None |
|UInt32 |NPY_UINT32 |None |
|UInt64 |NPY_UINT64 |None |
|Int8 |NPY_INT8 |None |
|Int16 |NPY_INT16 |None |
|Int32 |NPY_INT32 |None |
|Int64 |NPY_INT64 |None |
|Float32 |NPY_FLOAT32 |None |
|Float64 |NPY_FLOAT64 |None |
|Decimal32 |Cast to Float |None |
|Decimal64 |Cast to Float |None |
|UUID |NPY_STRING |Fixed length of 16 bytes |
|Date |NPY_UINT16 |https://numpy.org/doc/stable/reference/arrays.datetime.html |
|DateTime |NPY_UINT32 |None |
|String |NPY_STRING |None |
|FixedString |NPY_STRING |None |
|Nullable |masked array |https://numpy.org/doc/stable/reference/maskedarray.html |
|Array |ndarray |Only supports Array inputs. https://numpy.org/doc/stable/reference/generated/numpy.ndarray.html |


<span id="ba0e0350"></span>
### Syntax

<span id="e6311442"></span>
#### Create Function

```SQL
CREATE FUNCTION function_name [TYPE udf_type] [RETURNS data_type] [FLAGS flags] LANGUAGE PYTHON AS
$custom_tag$

class function_name():
    def entry(self, output, inputs):
        expression
        
$custom_tag$

# udf_type: SCALAR (default), AGGREGATE (Not supported for current release)
# data_type: use the type of the first input column if not set, check 'Data Types' section above for all supported types
```



* $custom_tag$


Between the $$ symbols, you can use any custom tag or leave it blank, just make sure to close it again with the same tag. (See [PostgreSQL ](https://www.postgresql.org/docs/9.4/sql-syntax-lexical.html)4.1.2.4)

For example, here are two different ways to specify the string "Dianne's horse":

```Plain
$$Dianne's horse$$
$SomeTag$Dianne's horse$SomeTag$
```


All content within $tag$ is treated as Python code. Python syntax checks are not performed during the creation of Python UDFs.

<span id="a02d4358"></span>
#### DROP function

```SQL
DROP FUNCTION [IF EXISTS] function_name; 
```



* `IF EXISTS` is optional, it can prevent errors if the function does not exist. Under normal circumstances, if a function does not exist and you attempt to delete it, the system will report an error.


<span id="4af0d7f4"></span>
#### SHOW function

View all UDF functions.

```SQL
SHOW functions;  -- View all UDF
-- DESCRIBE FUNCTION udf_name; --- View the specified UDF
```


<span id="ddaa3179"></span>
#### SHOW CREATE function

View the definition of a specific UDF.

```SQL
SHOW CREATE FUNCTION udf_name; 
```


<span id="da0ff5c6"></span>
#### SELECT function

A UDF works the same as any other function in ByteHouse, but you need to specify theto access it.

For example, to use the UDF that calculates the area of a circle:

```SQL
drop function if exists test.area_of_circle;

CREATE FUNCTION test.area_of_circle RETURNS Float64 LANGUAGE PYTHON AS
$pikachu$
from iudf import IUDF
from overload import overload
from math import pi

class area_of_circle(IUDF):
    @overload
    def process(radius):
        return radius*radius*pi
$pikachu$;
```


<span id="4b3de2c1"></span>
### Usage Example

<span id="4b3c375e"></span>
#### Example 1

This UDF example adds the values of each row in this table and outputs the result.


* Databases and Tables Required to Create UDF

   ```SQL
   CREATE DATABASE test;
    
   CREATE TABLE test.test_udf_int
   (
       a Int64,
       b Int64,
       c Int64,
       d Int64
   )
   ENGINE = CnchMergeTree()
   PRIMARY KEY a
   ORDER BY a;
   
   INSERT INTO test.test_udf_int(a, b, c, d)
   VALUES (0, 0, 0, 0 ) (1, 1, 1, 1) (2, 2, 2, 2);
   ```
   

* Create UDF

   Next, create the UDF function using CREATE FUNCTION. Here is an example of how to write an entry function in Python, using [code] as a separator.

   Although ByteHouse is a column\-based database, you generally want to calculate each row. In this example, the entry function uses an iterator to loop through each row and sum the four input values in each row to obtain the output value.

   ```SQL
   CREATE FUNCTION f_plus_int RETURNS Int64 LANGUAGE PYTHON AS
   $code$
   import numpy as np
   
   class f_plus_int:
       def entry(self, output, inputs):
           nargs = len(inputs)
   
           it = np.nditer([output] + inputs,
                   ['refs_ok', 'buffered'], [['writeonly']] + [['readonly']]*nargs)
   
           with it:
               for out, *ins in it:
                   out[...] = self.process(*[x.item() for x in ins])
                   
       def process(self, x1, y1, x2, y2):
          return x1 + y2 + x2 + y2
          
   $code$;
   ```
   

   Alternatively, you can use the fully column\-based method provided by Python Numpy. It performs the same actions as `f_plus_int`.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The performance of using the column\-based method is superior to using loops.   </div>
   

   ```SQL
   CREATE FUNCTION f_plus_int RETURNS Int64 LANGUAGE PYTHON AS
   $code$
   import numpy as np
   
   class f_plus_int:
       def entry(self, output, inputs):
           np.add.reduce(inputs, out=output)
   $code$;
   ```
   

* Invoke UDF

   Once a Python UDF function is created, it can be called like any ordinary built\-in function.

   ```SQL
   select f_plus_int(a,b,c,d) from test.test_udf_int;
   ```
   

* Return Result

   ```Plain
   ┌─f_plus_int(a, b, c, d)─┐
   │                           0 │
   │                           4 │
   │                           8 │
   └─────────────────────────────┘
   ```
   

* Delete UDF

   ```SQL
   drop function f_plus_int;
   ```
   


<span id="81dea6b8"></span>
#### Example 2


* Create Database and Table for UDF

   ```SQL
   CREATE TABLE test.py_fixedstring
   (
       a FixedString(2),
       b FixedString(3)
   ) 
   ENGINE = CnchMergeTree()
   ORDER BY b;
   
   INSERT INTO test.py_fixedstring(a, b)
   VALUES ('aa', 'aaa') ('bb', 'bbb') ('cc', 'ccc') ('dd', 'ddd') ('ee', 'eee') ('ff', 'fff') ('gg', 'ggg') ('ab', 'abc') ('cb', 'cba') ('tt', 'zzz');
   ```
   

* Create UDF

   For return types like `FixedString`, you must specify the length of the return string.

   ```SQL
   CREATE FUNCTION py_fixed_string
   RETURNS FixedString(5)
   LANGUAGE PYTHON AS
   $code$
   import numpy as np
   
   class py_fixed_string:
       def entry(self, output, inputs):
           nargs = len(inputs)
   
           it = np.nditer([output] + inputs,
                   ['refs_ok', 'buffered'], [['writeonly']] + [['readonly']]*nargs)
   
           with it:
               for out, *ins in it:
                   out[...] = self.process(*[x.item() for x in ins])
   
       def process(self, a, b):
           return a + b
   $code$; 
   ```
   

* Invoke UDF

   ```SQL
   select py_fixed_string(a, b) from test.py_fixedstring; 
   ```
   

* Return results

   ```SQL
   ┌─py_fixed_string(a, b)─┐
   │ aaaaa                      │
   │ ababc                      │
   │ bbbbb                      │
   │ cbcba                      │
   │ ccccc                      │
   │ ddddd                      │
   │ eeeee                      │
   │ fffff                      │
   │ ggggg                      │
   │ ttzzz                      │
   └────────────────────────────┘
   ```
   

* Delete UDF

   ```SQL
   drop function py_fixedstring; 
   ```
   


<span id="1039eb56"></span>
#### Overload

Additionally, ByteHouse offers overload.py, which allows you to create multiple UDFs in a single statement. Each function can accept different parameters as inputs, as shown:

```SQL
CREATE FUNCTION f_plus_int
RETURNS Date
LANGUAGE PYTHON AS
$code$
from iudf import IUDF
from overload import overload
 
class f_plus_int(IUDF):
    @overload
    def process(a): 
        return a + 1

    @overload
    def process(a, b):
        return a + b
$code$;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">@overload is a decorator that wraps functions and returns a callable object of Function Type. If using this entry function, the decorator @overload must be used in the function. It needs to be called from the entry point to avoid parameter number mismatch errors.</div>


<span id="ff94406a"></span>
### Pre\-installed environment dependencies

The current environment comes pre\-installed with the following dependencies:

```Shell
agate==1.6.3
aiohttp==3.8.3
aiosignal==1.3.1
async-timeout==4.0.2
asynctest==0.13.0
attrs==22.1.0
Babel==2.11.0
base58==2.1.1
bitarray==2.6.0
certifi==2022.6.15
cffi==1.15.1
charset-normalizer==2.1.0
click==8.1.3
clickhouse-connect==0.4.0
clickhouse-driver==0.2.4
colorama==0.4.5
cytoolz==0.12.0
dbt-clickhouse==1.3.0
dbt-core==1.3.0
dbt-extractor==0.4.1
eth-abi==3.0.1
eth-account==0.7.0
eth-hash==0.3.3
eth-keyfile==0.6.0
eth-keys==0.4.0
eth-rlp==0.3.0
eth-typing==3.2.0
eth-utils==2.0.0
ethereum-abi-utils==0.4.7
ethereum-tester==0.1.0b3
ethereum-utils==0.6.2
frozenlist==1.3.3
future==0.18.2
hexbytes==0.3.0
hologram==0.0.15
idna==3.3
importlib-metadata==5.0.0
ipfshttpclient==0.7.0
isodate==0.6.1
Jinja2==3.1.2
jsonschema==3.2.0
leather==0.3.4
llvmlite==0.39.1
Logbook==1.5.3
lru-dict==1.1.8
MarkupSafe==2.1.1
mashumaro==3.0.4
minimal-snowplow-tracker==0.0.2
msgpack==1.0.4
multiaddr==0.0.9
multidict==6.0.2
netaddr==0.8.0
networkx==2.8.8
numba==0.56.4
numpy==1.23.2
packaging==21.3
pandas==1.5.1
parsedatetime==2.4
parsimonious==0.8.1
pathspec==0.9.0
protobuf==4.21.9
pycparser==2.21
pycryptodome==3.15.0
pylru==1.2.1
pyparsing==3.0.9
pyrsistent==0.19.2
pysha3==1.0.2
python-dateutil==2.8.2
python-slugify==6.1.2
pytimeparse==1.1.8
pytz==2022.6
pytz-deprecation-shim==0.1.0.post0
PyYAML==6.0
requests==2.28.1
rlp==3.0.0
scipy==1.9.3
six==1.16.0
sqlparse==0.4.3
text-unidecode==1.3
toolz==0.12.0
typing_extensions==4.4.0
tzdata==2022.6
tzlocal==4.2
urllib3==1.26.11
varint==1.0.2
web3==3.16.3
websockets==10.4
Werkzeug==2.2.2
yarl==1.8.1
zipp==3.10.0
```


&nbsp;
