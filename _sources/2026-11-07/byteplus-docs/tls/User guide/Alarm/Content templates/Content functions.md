---
title: "Content functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/content_functions"
---

Log Service provides a series of functions for processing alarm notification content, allowing you to perform various transformations and operations on data and variables through these functions. This document explains the syntax, usage, and examples of the built\-in functions provided by Log Service.

<span id="3b18e637"></span>
## Control functions


|Function |syntax |Example |
|---|---|---|
|until |the until function generates an Integer array from 0 to n with a default step of 1, similar to the range function in python. for example, `until(3)` returns the array `[]int{0,1,2}`.<br><br>supports use with for loops.<br><br>syntax format is as follows:<br><br>```Python```<br>```until(n)```<br><br><br>where n is the array length of Integer type. |* function examples<br><br>   ```Python```<br>```   {%for i in until(3)%}```<br>```   {{i}}```<br>```   {%endfor%}```<br>```   ```<br>   <br><br>* processing results<br><br>   ```Python```<br>```   0```<br>```   1```<br>```   2```<br>```   ```<br>    |
|untilStep |the untilStep function generates an Integer array from start to stop (excluding stop) with a step size of step.<br><br>syntax format is as follows:<br><br>```Python```<br>```untilStep(start,stop,step)```<br><br><br>note:<br><br><br>* start: Integer type, representing the left boundary of the array.<br><br>* Stop: an Integer representing the array's right boundary.<br><br>* Step: an Integer representing the array step size. |* Function example<br><br>   ```Python```<br>```   {%for i in untilStep(0,10,2)%}```<br>```   {{i}}```<br>```   {%endfor%}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   0 2 4 6 8```<br>```   ```<br>    |


<span id="09ae0a04"></span>
## UUID functions


|function |Syntax |Example |
|---|---|---|
|uuidv4 |The uuidv4 function generates a random string using the UUID v4 algorithm.<br><br>The syntax is as follows:<br><br>```Python```<br>```{{uuidv4()}}```<br> |* Function example<br><br>   ```Python```<br>```   {{uuidv4()}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   2b1ac53a-413c-428a-b35d-48c62a12d86d```<br>```   ```<br>    |


<span id="f4bfcd8d"></span>
## URL functions


|function |syntax |Example |
|---|---|---|
|urlParse |The urlParse function extracts specified fields from a URL, returning the result as a string.<br><br>The syntax format is as follows:<br><br>```SQL```<br>```{{urlParse(url)}}```<br><br><br>Where url represents the URL string from which to extract fields. |extract a URL string into the following format.<br><br>```JSON```<br>```{```<br>```scheme:   'http'```<br>```host:     'server.com:8080'```<br>```path:     '/api'```<br>```query:    'list=false'```<br>```opaque:   nil```<br>```fragment: 'anchor'```<br>```userinfo: 'admin:secret'```<br>```}```<br><br><br><br>* function example<br><br>   <PreCode lang="Python" text={`{{ urlParse("http://admin:secret@server.com:8080/api?list=false#anchor")}} \n toJson(urlParse("http://admin:secret@server.com:8080/api?list=false#anchor"))`}\><br><br>* Processing result<br><br>   ```YAML```<br>```   {%with t=urlParse("http://admin:secret@server.com:8080/api?list=false#anchor")%}```<br>```      {{t.scheme}}```<br>```      {{t.host}}```<br>```      {{t.path}}```<br>```       {{t.query}}```<br>```       {{t.opaque}}```<br>```       {{t.fragment}}```<br>```   {%endwith%}```<br>```   ```<br>    |
|urlJoin |urlJoin converts a URL object into string form.<br><br>Grammar format is as follows:<br><br>```SQL```<br>```{{urlJoin(urlObj)}}```<br><br><br>Here, urlObj represents the object containing URL information. |* function example<br><br>   ```Python```<br>```   {{urlJoin(dict("fragment","fragment","host","host:80","path","/path","query","query","scheme","http"))}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Plain```<br>```   http://host:80/path?query#fragment```<br>```   ```<br>    |


<span id="0906809c"></span>
## Math functions


|function name |Syntax description |Example |
|---|---|---|
|max |The max function returns the maximum value among all parameters.<br><br>Syntax format is as follows:<br><br>```Python```<br>```max(value=a,b,c,d,e...)```<br> |* Function example<br><br>   ```Python```<br>```   {{max(1,2,3,4)}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   4```<br>```   ```<br>    |
|min |the min function returns the smallest value among all parameters.<br><br>syntax format is as follows:<br><br>```Python```<br>```min(value=a,b,c,d,e...)```<br> |* function example<br><br>   ```Python```<br>```   {{min(3,5,3,1)}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   1```<br>```   ```<br>    |
|ceil |The ceil function rounds data up to the nearest integer.<br><br>The syntax format is as follows:<br><br>```Python```<br>```ceil(value=data)```<br> |* function example<br><br>   ```Python```<br>```   {{ceil(1.1)}}```<br>```   ```<br>   <br><br>* result<br><br>   ```Python```<br>```   2.000000```<br>```   ```<br>    |
|floor |The floor function rounds data down<br><br>The syntax format is as follows:<br><br>```Python```<br>```floor(value=data)```<br> |* function example<br><br>   ```Python```<br>```   {{floor(1.1)}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   1.000000```<br>```   ```<br>    |
|add |The add function performs addition by treating all input parameters as Integer type and summing them.<br><br>Syntax format is as follows:<br><br>```Python```<br>```add(value=a,b,c,d...)```<br> |* Function example<br><br>   ```Python```<br>```   add(1,2,3)```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   6```<br>```   ```<br>    |
|sub |The sub function performs subtraction, outputting `a - b`, where both a and b are Integers.<br><br>The syntax format is as follows:<br><br>```Python```<br>```sub(a,b)```<br> |* Function example<br><br>   ```Python```<br>```   sub(10,1)```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   9```<br>```   ```<br>    |
|div |The div function performs division, that is, `a/b`.<br><br>Grammar format is as follows:<br><br>```Python```<br>```div(a,b)```<br> |* function example<br><br>   ```Python```<br>```   div(10,2)```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   5```<br>```   ```<br>    |
|mod |mod function returns the remainder, i.e., `a%b`.<br><br>Syntax format is as follows:<br><br>```Python```<br>```mod(a,b)```<br> |* function example<br><br>   ```Python```<br>```   mod(10,3)```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   1```<br>```   ```<br>    |
|mul |The mul function performs multiplication, calculating the product of all input parameters, and returns an Integer type result.<br><br>The syntax format is as follows:<br><br>```Python```<br>```mul(value=a,b,c,...)```<br> |* Function example<br><br>   ```Python```<br>```   mul(1,2,3)```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   6```<br>```   ```<br>    |
|round |The round function rounds a numerical value. Outputs the rounded value with six decimal places.<br><br>Grammar format is as follows:<br><br>```Python```<br>```round(data,i,j)```<br><br><br>Note:<br><br><br>* data: float type, represents the original value.<br><br>* i: Integer type, indicates the digit position for rounding. Positive integers represent decimal places; negative integers represent digits before the decimal point.<br><br>* j: float type, range (0,1), rounds up only if the fractional part of data is greater than j; otherwise, it truncates. |* function example<br><br>   ```Python```<br>```   {{round(1.1,0,0.5)}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   1.000000```<br>```   ```<br>    |


<span id=".5a2X56ym5Liy5Ye95pWw"></span>
## String functions


|function |Description |Usage examples |
|---|---|---|
|trim |The trim function removes whitespace from the beginning and end of the original string.<br><br>Syntax format is as follows:<br><br>```Python```<br>```trim(value)```<br> |* Function example<br><br>   ```Python```<br>```   {{trim(" a ")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   a```<br>```   ```<br>    |
|upper |the upper function converts all characters in the original string to uppercase.<br><br>the syntax is as follows:<br><br>```Python```<br>```upper(value)```<br> |* Function examples<br><br>   ```Python```<br>```   {{upper("hello")}}```<br>```   ```<br>   <br><br>* Processing results<br><br>   ```Python```<br>```   HELLO```<br>```   ```<br>    |
|lower |the lower function converts all characters in the original string to lowercase.<br><br>syntax is as follows:<br><br>```Python```<br>```lower(value)```<br> |* Function example<br><br>   ```Python```<br>```   {{lower("HELLO")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   hello```<br>```   ```<br>    |
|title |The title function converts the original string to title case, capitalizing the first letter of each word and lowercasing the rest.<br><br>Syntax format:<br><br>```Python```<br>```title(value)```<br> |* Function example<br><br>   ```Python```<br>```   {{title("hello world")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   Hello World```<br>```   ```<br>    |
|contains |contains function checks if the specified string `originstr` contains the substring `substr`. If it contains the specified substring, it returns True; otherwise, it returns False.<br><br>Syntax is as follows:<br><br>```Python```<br>```contains(substr,orignstr)```<br><br><br>Note:<br><br><br>* originstr: a string representing the string to be checked.<br><br>* substr: a string representing the substring. |* function example<br><br>   ```Python```<br>```   {{contains("hel","hello")}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   True```<br>```   ```<br>    |
|quote |The quote function wraps the specified string in half\-width double quotes ("").<br><br>The syntax format is as follows:<br><br>```Python```<br>```quote (value)```<br> |* Function example<br><br>   ```Python```<br>```   {{quote("hello\"")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   "hello""```<br>```   ```<br>    |
|replace |The replace function replaces a substring `oldstr` in the specified string `originstr` with another substring `newstr`. The output format is a string.<br><br>Syntax is as follows:<br><br>```Python```<br>```replace(oldstr,newstr,originstr)```<br><br><br>Note:<br><br><br>* originstr: string type, representing the original string.<br><br>* oldstr: string type, representing the original substring to be replaced.<br><br>* newstr: string type, representing the new substring for replacement. |* Function example<br><br>   ```Python```<br>```   {{replace("ll","aa","hello")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   heaao```<br>```   ```<br>    |
|repeat |The repeat function generates a repeated sequence by repeating a string n times. The output result is in string format.<br><br>Syntax format is as follows:<br><br>```Python```<br>```repeat(n,str)```<br><br><br>Note:<br><br><br>* n: Integer type, indicating the number of repetitions.<br><br>* str: String type, representing the original string. |* function example<br><br>   ```Python```<br>```   {{repeat(3,"hello")}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   hellohellohello```<br>```   ```<br>    |
|substr |the substr function extracts the substring from `str` at the index range [i,j). the output is the extracted keyword in string format.<br><br>the syntax format is as follows:<br><br>```Python```<br>```substr(i,j,str)```<br><br><br>Note:<br><br><br>* i: Integer type, the left boundary index of the substring, starting from zero.<br><br>* j: Integer type, the right boundary of the substring, excluding j.<br><br>* str: String type, representing the original string. |* function example<br><br>   ```Python```<br>```   {{substr(0,5,"hello world")}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   hello```<br>```   ```<br>    |
|nospace |The nospace function removes all spaces from the string `str`.<br><br>The syntax is as follows:<br><br>```Python```<br>```nospace(str)```<br><br><br>Here, str is a string type representing the original string. |* function example<br><br>   ```Python```<br>```   {{nospace("hello world")}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   helloworld```<br>```   ```<br>    |
|trunc |The trunc function extracts the substring [0,i) from string `str` and returns the result. The output is the extracted substring.<br><br>The syntax is as follows:<br><br>```Python```<br>```trunc(i,str)```<br><br><br>Note:<br><br><br>* i: Integer type, representing the right boundary of the string, excluding i.<br><br>* str: String type, representing the original string. |* Function example<br><br>   ```Python```<br>```   {{trunc(5,"hello world")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   hello```<br>```   ```<br>    |
|abbrev |the abbrev function truncates a specified string. this function requires specifying the truncated string length, with other characters replaced by ellipsis (...). the output format is a string type.<br><br>the syntax format is as follows:<br><br>```Python```<br>```abbrev(i,str)```<br><br><br>Note:<br><br><br>* i: an Integer type representing the substring retained from positions [0, i).<br><br>* str: a string type representing the original string. |* function example<br><br>   ```Python```<br>```   {{abbrev(8,"hello world")}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   hello...```<br>```   ```<br>    |
|abbrevboth |The abbrevboth function keeps the `str` substring between [i,j), replacing the rest of the string with .... The output format is string type.<br><br>The syntax is as follows:<br><br>```Python```<br>```abbrevboth(i,j,str)```<br><br><br>Note:<br><br><br>* i and j: Integer type, indicating the substring range [i,j) to retain.<br><br>* Str: string type, representing the original string. |* Function example<br><br>   ```Python```<br>```   {{abbrevboth(5,10,"hello world!!!")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   ... wor...```<br>```   ```<br>    |
|initials |the initials function extracts the first letter of each word in the string `str` and combines them into a new string.<br><br>the syntax is as follows:<br><br>```Python```<br>```initials(str)```<br> |* Function example<br><br>   ```Python```<br>```   {{initials("hello world!!!")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   hw```<br>```   ```<br>    |
|randAlphaNum |the randAlphaNum function generates a random string containing numbers. the output format is a string type.<br><br>the syntax format is as follows:<br><br>```Python```<br>```randAlphaNum(n)```<br><br><br>Here, n is an integer representing the number of characters. |* Function example<br><br>   ```Python```<br>```   {{randAlphaNum(1)}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   5```<br>```   ```<br>    |
|randAlpha |The randAlpha function generates a random string without numbers.<br><br>The syntax is as follows:<br><br>```Python```<br>```randAlpha(n)```<br><br><br>Where n is an Integer representing the number of characters. |* Function example<br><br>   ```Python```<br>```   {{randAlpha(1)}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   c```<br>```   ```<br>    |
|randNumeric |randNumeric generates random numbers. The output result is a string.<br><br>The syntax format is as follows:<br><br>```Python```<br>```randNumeric(n)```<br><br><br>Here, n is an integer representing the number of characters. |* Function example<br><br>   ```Python```<br>```   {{randNumeric(3)}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   321```<br>```   ```<br>    |
|randAscii |the andAscii function generates random ARSCII characters. the output is a string.<br><br>the syntax format is as follows:<br><br>```Python```<br>```randAscii(n)```<br><br><br>where n is an integer representing the number of characters. |* function example<br><br>   ```Python```<br>```   {{randAscii(3)}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   i&g```<br>```   ```<br>    |
|hasPrefix |hasPrefix function is used to determine whether the specified string contains the specified prefix. Returns True if it contains, otherwise returns False.<br><br>The syntax is as follows:<br><br>```Python```<br>```hasPrefix(pre,str)```<br><br><br>Note:<br><br><br>* pre: string type, indicating the string prefix.<br><br>* str: string type, indicating the original string. |* function example<br><br>   ```Python```<br>```   {{hasPrefix("hel","hello")}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   True```<br>```   ```<br>    |
|hasSuffix |The hasSuffix function checks whether a specified string contains a given suffix. Returns True if it contains the suffix; otherwise, returns False.<br><br>The syntax format is as follows:<br><br>```Python```<br>```hasSuffix(suf,str)```<br><br><br>Note:<br><br><br>* suf: string type, representing the string suffix.<br><br>* str: a string type representing the original string. |* Function example<br><br>   ```Python```<br>```   {{hasSuffix("llo","hello")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   True```<br>```   ```<br>    |
|squote |The squote function escapes a string and wraps it in single quotes (''). The output format is a string type.<br><br>The syntax format is as follows:<br><br>```Python```<br>```squote(str)```<br><br><br>Here, str is a string type representing the original string. |* Function example<br><br>   <PreCode lang="Python" text={`{{squote("hello\"")}}`}\><br><br>* Processing result<br><br>   ```Python```<br>```   'hello"'```<br>```   ```<br>    |
|cat |The cat function concatenates specified strings. The output format is a string.<br><br>Syntax is as follows:<br><br>```Python```<br>```cat(data=a,b,c)```<br><br><br>a, b, and c are all string types representing the characters to be concatenated. |* function example<br><br>   <PreCode lang="Python" text={`{{cat("hello",1,true)}}`}\><br><br>* processing result<br><br>   ```Python```<br>```   hello 1 true```<br>```   ```<br>    |
|indent |the indent function aligns a string by adding spaces before the specified string.<br><br>the syntax format is as follows:<br><br>```Python```<br>```indent(n,str)```<br><br><br>Here, n represents the number of additional spaces, and str is the original string. |* Function example<br><br>   ```Python```<br>```   {{indent(3,"hello")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```      hello```<br>```   ```<br>    |
|nindent |The nindent function aligns a string after a line break by adding n spaces following the line break.<br><br>The syntax format is as follows:<br><br>```Python```<br>```nindent(n,str)```<br> |* Function example<br><br>   ```Python```<br>```   {{nindent(3,"hello")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   ```<br>```      hello```<br>```   ```<br>    |
|plural |The plural function performs conditional judgment; it returns the first argument if parameter i equals 1, otherwise it returns the second argument.<br><br>Syntax format:<br><br>```Python```<br>```plural(a,b,i)```<br> |* function example<br><br>   ```Python```<br>```   {{plural("a","b",1)}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   a```<br>```   ```<br>    |
|snakecase |snakecase function converts naming conventions to underscore\-separated naming.<br><br>The syntax is as follows:<br><br>```Python```<br>```snakecase(str)```<br> |* Function example<br><br>   ```Python```<br>```   {{snakecase("HelloWorld")}}```<br>```   ```<br>   <br><br>* Processing results<br><br>   ```Python```<br>```   hello_world```<br>```   ```<br>    |
|camelcase |The camelcase function converts naming conventions to UpperCamelCase.<br><br>Syntax format is as follows:<br><br>```Python```<br>```camelcase(str)```<br> |* Function examples<br><br>   ```Python```<br>```   {{camelcase("hello_world")}}```<br>```   ```<br>   <br><br>* Processing results<br><br>   ```Python```<br>```   HelloWorld```<br>```   ```<br>    |
|kebabcase |The kebabcase function converts naming conventions into kebab case separated by hyphens (\-).<br><br>The syntax format is as follows:<br><br>```Python```<br>```kebabcase(str)```<br> |* example 1<br><br>   * function example<br><br>      ```Python```<br>```      {{kebabcase("hello_world")}}```<br>```      ```<br>      <br><br>   * processing result<br><br>      ```Python```<br>```      hello-world```<br>```      ```<br>      <br><br>* example 2<br><br>   * function example<br><br>      ```Python```<br>```      {{kebabcase("FirstName")}}```<br>```      ```<br>      <br><br>   * processing result<br><br>      ```Python```<br>```      first-name```<br>```      ```<br>       |
|swapcase |The swapcase function converts the case of characters in a string.<br><br>Syntax is as follows:<br><br>```Python```<br>```swapcase(str)```<br> |* function example<br><br>   ```Python```<br>```   {{swapcase("HelloWorld")}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   hELLOwORLD```<br>```   ```<br>    |
|shuffle |the shuffle function rearranges the characters in the original string into a new string randomly.<br><br>the syntax is as follows:<br><br>```Python```<br>```shuffle(syr)```<br> |* function example<br><br>   ```Python```<br>```   {{shuffle("HelloWorld")}}```<br>```   ```<br>   <br><br>* result<br><br>   ```Python```<br>```   dHrollelWo```<br>```   ```<br>    |


<span id=".5a-56LGh5ZKM5YiX6KGo5Ye95pWw"></span>
## Object and list functions


|function |Description |usage examples |
|---|---|---|
|join |the join function connects specified elements in the value list using a delimiter. The connector can be specified using the symbol parameter.<br><br>The syntax format is as follows:<br><br>```Python```<br>```join(symbol='',value)```<br> |* Example 1<br><br>   * Function example<br><br>      ```Python```<br>```      {{ join("",list(1, 2, 3)) }}```<br>```      ```<br>      <br><br>   * processing result<br><br>      ```Python```<br>```      123```<br>```      ```<br>      <br><br>* example 2<br><br>   * function example<br><br>      ```Python```<br>```      {{ join(',',list(1, 2, 3)) }}```<br>```      ```<br>      <br><br>   * processing result<br><br>      ```Python```<br>```      1,2,3```<br>```      ```<br>       |
|split |The split function is used to divide the specified string value. The result is an object type. The key is _i, a string type where i represents the index.<br><br>Syntax format:<br><br>```Python```<br>```split(symbol,value)```<br><br><br>Note:<br><br><br>* symbol: a string type used to specify the delimiter.<br><br>* value: a string type representing the original string to be split. |* Function example<br><br>   ```Python```<br>```   {%for k,v in split(",","a,b,c")%}```<br>```   {{k}}:{{v}}```<br>```   {%endfor%}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   _0:a```<br>```   _1:b```<br>```   _2:c```<br>```   ```<br>    |
|toString |toString function converts the specified parameter to string format.<br><br>Syntax is as follows:<br><br>```Python```<br>```toString(value)```<br> |* Function example<br><br>   ```Python```<br>```   {{toString("aa")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   aa```<br>```   ```<br>    |
|toJson |The toJson function converts the specified parameter into a JSON\-formatted string output.<br><br>The syntax format is as follows:<br><br>```Python```<br>```toJson(value)```<br> |* function example<br><br>   ```Python```<br>```   {{toJson(urlParse("http://admin:secret@server.com:8080/api?list=false#anchor"))}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   {"fragment": "anchor","host": "server.com:8080","hostname": "server.com","opaque": "","path": "/api","query": "list=false","scheme": "http","userinfo": "admin:secret"}```<br>```   ```<br>    |
|toPrettyJson |toPrettyJson converts the specified parameter into a formatted string.<br><br>The syntax format is as follows:<br><br>```Python```<br>```toPrettyJson(value)```<br> |* Function example<br><br>   ```Python```<br>```   {{toPrettyJson(urlParse("http://admin:secret@server.com:8080/api?list=false#anchor"))}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```JSON```<br>```   {```<br>```     "fragment": "anchor",```<br>```     "host": "server.com:8080",```<br>```     "hostname": "server.com",```<br>```     "opaque": "",```<br>```     "path": "/api",```<br>```     "query": "list=false",```<br>```     "scheme": "http",```<br>```     "userinfo": "admin:secret"```<br>```   }```<br>```   ```<br>    |
|ternary |The ternary function performs conditional judgment. It returns value1 if value3 is true; otherwise, it returns value2.<br><br>Grammar format is as follows:<br><br>```Python```<br>```ternary(value1,value2,value3)```<br> |* function example<br><br>   ```Python```<br>```   {{ternary(1,2,true)}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   1```<br>```   ```<br>    |
|append |The append function adds a specified value to a list, that is, it adds the value to list1.<br><br>The syntax format is as follows:<br><br>```Python```<br>```append(list1,value)```<br> |* function example<br><br>   ```Python```<br>```    {%-with mp1=list("a","1","b","2")-%}```<br>```    {%-with mp1=append(mp1,"a")%}```<br>```    {{-mp1```<br>```    {%endwith-%}```<br>```    {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   a,1,b,2,a```<br>```   ```<br>    |


<span id=".5pWw5o2u57uT5p6E"></span>
## Data structure functions


|function |Description |Usage examples |
|---|---|---|
|list |the list function defines the specified parameter as a list.<br><br>the syntax format is as follows:<br><br>```Python```<br>```list(values=a,b,c,...)```<br> |* function example<br><br>   ```Python```<br>```   {{list("a","b","c")```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   a,b,c```<br>```   ```<br>    |
|dict |The dict function defines parameters as a key\-value JSON object and returns it, similar to direct usage`{}`Create a dictionary.<br><br>The syntax format is as follows:<br><br>```Python```<br>```dict(key1,value1,key2,value2)```<br> |* function example<br><br>   ```Python```<br>```   {{toJson(dict("a",1,"b",2))}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```JSON```<br>```   {"a":1,"b":2}```<br>```   ```<br>    |
|hasKey |the hasKey function checks whether the dictionary dict contains the specified key.<br><br>the syntax format is as follows:<br><br>```Python```<br>```hasKey(dict,key)```<br> |* Function example<br><br>   ```Python```<br>```   {%with mp=dict("a",1,"b",2)%}```<br>```   {%if hasKey(mp,"a")%}```<br>```   has```<br>```   {%else%}```<br>```   no```<br>```   {%endif%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   has```<br>```   ```<br>    |
|set |The set function assigns a value to a property in a dictionary.<br><br>The syntax is as follows:<br><br>```Python```<br>```dict(key，value)```<br> |* function example<br><br>   ```Python```<br>```   {%with mp=dict("a",1,"b",2)%}```<br>```   {%with mp=set(mp,"a",3)%}```<br>```   {%for k,v in mp%}```<br>```   {{k}}:{{v}}```<br>```   {%endfor%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   mp={"a":3,"b":2}```<br>```   ```<br>    |
|unset |The unset function deletes an attribute from a dictionary.<br><br>Syntax format:<br><br>```Python```<br>```unset(map,key)```<br><br><br>Note:<br><br><br>* map: field name,<br><br>* key: key of the attribute to be deleted. |* function example<br><br>   ```Python```<br>```   {%with mp=dict("a",1,"b",2)%}```<br>```   {%with mp=unset(mp,"a")%}```<br>```   {%for k,v in mp%}```<br>```   {{k}}:{{v}}```<br>```   {%endfor%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   mp={"b":2}```<br>```   ```<br>    |
|pluck |The pluck function constructs an array from the same key across multiple dictionaries.<br><br>The syntax format is as follows:<br><br>```Python```<br>```pluck(key,map1,map2)```<br> |* function example<br><br>   ```Python```<br>```   {%with mp1=dict("a",1,"b",2)%}```<br>```   {%with mp2=dict("a",2,"b",2)%}```<br>```       {%- for v in pluck("a",mp1,mp2) %}```<br>```           {{ v}}```<br>```       {%- endfor -%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   1```<br>```   2```<br>```   ```<br>    |
|merge |The merge function merges two dictionaries, producing their union.<br><br>Syntax format is as follows:<br><br>```Python```<br>```merge(map1,map2)```<br> |* function example<br><br>   ```Python```<br>```   {%with mp1=dict("a",1,"b",2)%}```<br>```   {%with mp2=dict("b",2,"d",2)%}```<br>```   {%with mp1=merge(mp1,mp2)%}```<br>```      {%- for k,v in mp1 -%}```<br>```      {{k}}:{{v}}```<br>```      {% endfor -%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   a:1```<br>```   b:2```<br>```   d:2```<br>```   ```<br>    |
|mergeOverwrite |the mergeOverwrite function merges two dictionaries, using the value from the second dictionary if keys duplicate.<br><br>the syntax is as follows:<br><br>```Python```<br>```mergeOverwrite(map1,map2)```<br> |* function example<br><br>   ```Python```<br>```   {%with mp1=dict("a","1","b","2")%}```<br>```   {%with mp2=dict("a","1","b","2")%}```<br>```   {%with mp1=mergeOverwrite(mp1,mp2)%}```<br>```      {%- for k,v in mp1 -%}```<br>```      {{k}}:{{v}}```<br>```      {% endfor -%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   a:1```<br>```   b:2```<br>```   ```<br>    |
|keys |The keys function retrieves the key list of a specified dictionary and returns it as an array.<br><br>The syntax is as follows:<br><br>```Python```<br>```keys(map1)```<br> |* function example<br><br>   ```Python```<br>```   {%with mp1=dict("a",1,"b",2)%}```<br>```   {%- for v in keys(mp1) -%}```<br>```   {{v}}```<br>```   {% endfor -%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   a```<br>```   b```<br>```   ```<br>    |
|values |The values function retrieves the list of values from a dictionary.<br><br>Syntax format is as follows:<br><br>```Python```<br>```values(map1)```<br> |* Function example<br><br>   ```Python```<br>```   {%with mp1=dict("a",1,"b",2)%}```<br>```   {%- for v in values(mp1) -%}```<br>```   {{v}}```<br>```   {% endfor -%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   1```<br>```   2```<br>```   ```<br>    |
|pick |Keep the specified key in the dictionary and save the key\-value pair as a new dictionary.<br><br>The syntax format is as follows:<br><br>```Python```<br>```pick(map1,key1,key2)```<br> |* function examples<br><br>   ```Python```<br>```   {%with mp1=dict("a",1,"b",2,"c","3")%}```<br>```   {%- for k,v in pick(mp1,"a","b") -%}```<br>```   {{-k}}:{{v}}```<br>```   {% endfor -%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing results<br><br>   ```Python```<br>```   a:1```<br>```   b:2```<br>```   ```<br>    |
|omit |Remove the specified key from the dictionary and save the remaining key\-value pairs as a new dictionary.<br><br>Syntax format is as follows:<br><br>```Python```<br>```omit(map,key)```<br> |* Function Example<br><br>   ```Python```<br>```   {%with mp1=dict("a",1,"b",2,"c",3)%}```<br>```   {%- for k,v in omit(mp1,"a") -%}```<br>```   {{-k}}:{{v}}```<br>```   {% endfor -%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Processing Result<br><br>   ```Python```<br>```   b:2```<br>```   c:3```<br>```   ```<br>    |
|deepCopy |The deepCopy function performs a deep copy of a variable.<br><br>The syntax format is as follows:<br><br>```Python```<br>```deepCopy(map1)```<br> |* Function example<br><br>   ```Python```<br>```   {%with mp1=dict("a",1,"b",2)%}```<br>```   {%with mp2=deepCopy(mp1)%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Processing result<br><br>   There are two dictionaries, mp1 and mp2, which have identical content and do not interfere with each other. |


<span id="be136f54"></span>
## Array manipulation functions


|function |Description |Usage examples |
|---|---|---|
|push |the push function adds a specified value to a list.<br><br>the syntax is as follows:<br><br>```Python```<br>```push(mp1,"x")```<br> |* Function example<br><br>   ```Python```<br>```   {%with mp1=list("a","1","b","2")%}```<br>```   {%with mp1=push(mp1,"x")%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   mp1=["a","1","b","2","x"]```<br>```   ```<br>    |
|prepend |The prepend function adds a value to the front of a list.<br><br>The syntax is as follows:<br><br>```Python```<br>```prepend(mp1,"x")```<br> |* Function example<br><br>   ```Python```<br>```   {%with mp1=list("a","1","b","2")%}```<br>```   {%with mp1=prepend(mp1,"x")%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Result<br><br>   ```Python```<br>```   mp1=["x","a","1","b","2"]```<br>```   ```<br>    |
|first |The first function returns the first element of the list.<br><br>Grammar format is as follows:<br><br>```Python```<br>```first(mp1)```<br> |* Function example<br><br>   ```Python```<br>```   {%with mp1=list("a","1","b","2")%}```<br>```   {{first(mp1)}}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   a```<br>```   ```<br>    |
|rest |The rest function returns all elements in a list except the first one.<br><br>The syntax format is as follows:<br><br>```Python```<br>```rest(mp1)```<br> |* Function example<br><br>   <PreCode lang="Python" text={`{%with mp1=list("a","1","b","2")%} \n {%with mp1=rest(mp1)%} \n {{toJson(mp1)}} \n {%endwith%} \n {%endwith%}`}\><br><br>* Processing result<br><br>   ```Python```<br>```   ["1","b","2"]```<br>```   ```<br>    |
|last |The last function returns the last element in a list.<br><br>The syntax format is as follows:<br><br>```Python```<br>```last(mp1)```<br> |* Function example<br><br>   ```Python```<br>```   {%with mp1=list("a","1","b","2")%}```<br>```   {{last(mp1)}}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   2```<br>```   ```<br>    |
|initial |initial function returns all elements except the last one.<br><br>Grammar format is as follows:<br><br>```Python```<br>```initial(mp1)```<br> |* function example<br><br>   <PreCode lang="Python" text={`{%with mp1=list("a","1","b","2")%} \n {%with mp1=initial(mp1)%} \n {{toJson(mp1)}} \n {%endwith%} \n {%endwith%}`}\><br><br>* processing result<br><br>   ```Python```<br>```   ```<br>```   ```<br>```   ["a","1","b"]```<br>```   ```<br>    |
|reverse |The reverse function reverses the order of a list.<br><br>Syntax format:<br><br>```Python```<br>```reverse(mp1)```<br> |* function example<br><br>   <PreCode lang="Python" text={`{%with mp1=list("a","1","b","2")%} \n {%with mp1=reverse(mp1)%} \n {{toJson(mp1)}} \n {%endwith%} \n {%endwith%}`}\><br><br>* processing result<br><br>   ```Python```<br>```   ```<br>```   ```<br>```   ["2","b","1","a"]```<br>```   ```<br>    |
|uniq |The uniq function removes duplicate parts from an array.<br><br>Syntax format is as follows:<br><br>```Python```<br>```uniq(mp1)```<br> |* function example<br><br>   ```Python```<br>```   {%with mp1=list("a","1","b","1")%}```<br>```   {%with mp1=uniq(mp1)%}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   mp1=["2","b","1"]```<br>```   ```<br>    |
|without |The without function extracts the non\-overlapping parts of two arrays. Given two arrays, a and b, it uses set difference to remove common elements and outputs the result.<br><br>Syntax format is as follows:<br><br>```Python```<br>```without(mp1,mp2)```<br> |* Function example<br><br>   ```Python```<br>```   {%with mp1=list("a","1","b","2")%}```<br>```   {%with mp2=list(1,"b",2)%}```<br>```   {{first(without(mp1,mp2))}}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   a```<br>```   ```<br>    |
|has |The has function checks whether an element exists in the array.<br><br>The syntax format is as follows:<br><br>```Python```<br>```has(key,mp1)```<br> |* Function example<br><br>   ```Python```<br>```   {%with mp1=list("a","1","b","2")%}```<br>```   {{has("a",mp1)}}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   True```<br>```   ```<br>    |
|slice |The slice function extracts values from a slice. The first parameter is a list, the second is the start index, and the third is the end index.<br><br>Syntax is as follows:<br><br>```Python```<br>```slice(map1, start index, end index)```<br> |* function example<br><br>   ```Python```<br>```   {%with mp1=list("a","1","b","2")%}```<br>```   {%for x in slice(mp1,0,2)%}```<br>```   {{x}}```<br>```   {%endfor%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   a```<br>```   1```<br>```   ```<br>    |
|concat |the concat function merges multiple arrays and saves them as a new array.<br><br>Syntax format is as follows:<br><br>```Python```<br>```concat(map1,map2)```<br> |* function example<br><br>   <PreCode lang="Python" text={`{%with mp1=list("a","1","b","2")%} \n {%with mp2=list("a","1","b","2")%} \n {%with mp3=concat(mp1,mp2)%} \n {{toJson(mp3)}} \n {%endwith%} \n {%endwith%} \n {%endwith%}`}\><br><br>* processing result<br><br>   ```Python```<br>```   mp3=["a","1","b","2","a","1","b","2"]```<br>```   ```<br>    |


<span id="7a62354e"></span>
## Date functions


|function |Description |Usage examples |
|---|---|---|
|date |The date function converts a specified timestamp into a string with the specified format.<br><br>Syntax format is as follows:<br><br>```Python```<br>```date("2006-01-02 15:04:05", Unix timestamp)```<br><br><br><br>* The first parameter represents the time format and must be specified as `2006-01-02 15:04:05`.<br><br>* `Unix timestamp`: the UTC time to be converted, defaults to the current time if omitted. This parameter is of Integer or time type. |* function example<br><br>   ```Python```<br>```   {{date("2006-01-02 15:04:05",now())}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   2023-11-16 16:26:20```<br>```   ```<br>    |
|dateInZone/date_in_zone |dateInZone/date_in_zone function retrieves the current time for a specified time zone.<br><br>The syntax format is as follows:<br><br>```Python```<br>```date_in_zone("2006-01-02 15:04:05", Unix timestamp, time zone)```<br><br><br><br>* The first parameter specifies the time format and must be set to (`2006-01-02 15:04:05`).<br><br>* `Unix timestamp`: the UTC time to convert, defaulting to the current moment.<br><br>* `Time zone`: the target time zone, converting UTC time to the specified time zone, such as `UTC+8`. Defaults to the current time zone. |* function example<br><br>   ```Python```<br>```   {{date_in_zone("2006-01-02 15:04:05","","UTC+8")}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   2023-11-16 16:26:20```<br>```   ```<br>    |
|date_modify/dateModify |The date_modify/dateModify function adds or subtracts time based on a given time, such as adding 20 minutes to the current time, and returns a time type.<br><br>Syntax format is as follows:<br><br>```Python```<br>```date_modify(time, Unix timestamp)```<br><br><br><br>* time: the amount of time to add or subtract, for example, +20m means add 20 minutes. Supported units include hours (h), minutes (m), and seconds (s).<br><br>* `Unix timestamp`: the UTC time to convert, defaulting to the current moment. You can also specify `now()` to represent the current time. |* function example<br><br>   ```Python```<br>```   date_modify("+20m",now())```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   2023-11-16 17:55:36.08687 +0800 CST m=+1200.191703835```<br>```   ```<br>    |
|now |The now function returns the current time as a time data type.<br><br>Grammar format is as follows:<br><br>```Python```<br>```now()```<br> |* function example<br><br>   ```Python```<br>```   now()```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   2023-11-16 17:36:38.006711 +0800 CST m=+0.200781293```<br>```   ```<br>    |
|ago |The ago function returns the time interval between the specified date and the current moment.<br><br>Syntax format:<br><br>```Python```<br>```ago (timestamp)```<br> |* function example<br><br>   ```Python```<br>```   ago(date_modify("+20m",now()))```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   -20m0s```<br>```   ```<br>    |


<span id="f0c04438"></span>
## Encryption functions


|function |Description |usage examples |
|---|---|---|
|sha256sum |The sha256sum function calculates the SHA256 value of the input string.<br><br>The syntax format is as follows:<br><br>```Python```<br>```sha256sum(string)```<br><br><br>Where string represents the string to be encoded. |* Function example<br><br>   ```Python```<br>```   {{sha256sum("hello")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824```<br>```   ```<br>    |
|sha1sum |The sha1sum function calculates the SHA1 value of the input string.<br><br>The syntax format is as follows:<br><br>```Python```<br>```sha1sum(string)```<br><br><br>Here, string represents the string to be encoded. |* Function example<br><br>   ```Python```<br>```   {{sha1sum("hello")}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   aaf4c61ddcc5e8a2dabede0f3b482cd9aea9434d```<br>```   ```<br>    |
|adler32sum |The adler32sum function returns the checksum using the Adler\-32 algorithm.<br><br>Grammar format is as follows:<br><br>```Python```<br>```adler32sum(string)```<br><br><br>Here, string refers to the string to be encoded. |* function example<br><br>   ```Python```<br>```   adler32sum("hello")```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   103547413```<br>```   ```<br>    |


<span id="3df78b14"></span>
## Reflect functions


|function |Description |Usage examples |
|---|---|---|
|typeOf |The typeOf function is used to get the type of a variable.<br><br>The syntax format is as follows:<br><br>```Python```<br>```typeOf(key)```<br> |* function example<br><br>   ```Python```<br>```   {{typeOf("a")}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   string```<br>```   ```<br>    |
|typeIs |The typeIs function checks whether a given string matches a specified format. Returns a Boolean data type.<br><br>The syntax is as follows:<br><br>```Python```<br>```typeIs(type,string)```<br><br><br>Note:<br><br><br>* type: format name, supports setting to Integer, string, etc., which corresponds to the printed value of the `fmt.Printf` function's `%T` parameter in golang.<br><br>* string: the string to be checked against the format. |* function example<br><br>   ```Python```<br>```   {{typeIs("int",1)}}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   True```<br>```   ```<br>    |
|kindOf |The kindOf function is used to determine the data type of the specified parameter.<br><br>Grammar format is as follows:<br><br>```Python```<br>```kindOf()```<br> |* Function example<br><br>   ```Python```<br>```   {{kindOf(1)}}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   int```<br>```   ```<br>    |
|deepEqual |The deepEqual function is used to reflectively determine if two values are equal. Returns a Boolean data type.<br><br>Syntax format is as follows:<br><br>```Python```<br>```deepEqual(value1,value2)```<br> |* function example<br><br>   ```Python```<br>```   {%with mp1=list("a","1","b","2")%}```<br>```   {%with mp2=list("a","1","b","2")%}```<br>```   {{deepEqual(mp1,mp2)}}```<br>```   {%endwith%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   True```<br>```   ```<br>    |


<span id="4757f7e1"></span>
## Regular expression functions


|function |Description |Usage examples |
|---|---|---|
|regexMatch |the regexMatch function determines whether the specified string matches the regular expression. returns true if it matches; otherwise, returns false.<br><br>equivalent to the MatchString function in Go language.<br><br>the syntax is as follows:<br><br>```Python```<br>```regexMatch(regex,string)```<br><br><br>note:<br><br><br>* regex: regular expression.<br><br>* string: the string to be checked. |* function example<br><br>   ```Python```<br>```   regexMatch("^Hello","Hello world")```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   True```<br>```   ```<br>    |
|regexFind |The regexFind function extracts content from a specified string using the designated regular expression, matching once.<br><br>Equivalent to the FindString function in Go language.<br><br>Syntax format is as follows:<br><br>```Python```<br>```regexFindAll(regex,string)```<br><br><br>Note:<br><br><br>* regex: regular expression.<br><br>* String: the string to be checked. |* Function Example<br><br>   ```Python```<br>```   regexFind("[abc]","abcd")```<br>```   ```<br>   <br><br>* Processing Result<br><br>   ```Python```<br>```   a```<br>```   ```<br>    |
|regexFindAll |The regexFindAll function extracts content from a specified string using a given regular expression, specifying the number of matches extracted.<br><br>Equivalent to the MatchString function in Go language.<br><br>Syntax format as follows:<br><br>```Python```<br>```regexFindAll(regex,string,n)```<br><br><br>Note:<br><br><br>* regex: a regular expression.<br><br>* String: the string to be judged.<br><br>* n: the number of matches. |* Function example<br><br>   ```Python```<br>```   {%with t=regexFindAll("[abc]","abca",4)%}```<br>```      {%for x in t%}```<br>```         {{x}}```<br>```   {%endfor%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Result<br><br>   ```Python```<br>```   a```<br>```   b```<br>```   c```<br>```   a```<br>```   ```<br>    |
|regexReplaceAll |The regexReplaceAll function replaces strings matching a regular expression with a specified string.<br><br>Equivalent to Go language's ReplaceAllString function.<br><br>The syntax format is as follows:<br><br>```Python```<br>```regexReplaceAll(regex,string1,string2)```<br><br><br>Note:<br><br><br>* regex: regular expression.<br><br>* string1: the string to be evaluated.<br><br>* string2: the replacement string. |* Function example<br><br>   ```Python```<br>```   regexReplaceAll("[abc]","abcd","")```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   d```<br>```   ```<br>    |
|regexSplit |The regexSplit function is equivalent to Golang `re.Split`, using a regular expression to split the string. The return data type is an array.<br><br>Syntax format:<br><br>```Python```<br>```regexSplit(regex,string,n)```<br><br><br>Note:<br><br><br>* regex: regular expression.<br><br>* String: the string to be evaluated.<br><br>* n: number of matches. |* Function example<br><br>   ```Python```<br>```   {%with t=regexSplit("[\\s]","1 2",2)%}```<br>```      {%for x in t%}```<br>```         {{x}}```<br>```      {%endfor%}```<br>```   {%endwith%}```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   1```<br>```   2```<br>```   ```<br>    |


<span id="811bb2ca"></span>
## Codec functions


|Function |Description |usage examples |
|---|---|---|
|b64enc |b64enc function encodes the specified string in Base64.<br><br>syntax format is as follows:<br><br>```Python```<br>```b64enc(string)```<br> |* Function example<br><br>   ```Python```<br>```   b64enc("hello")```<br>```   ```<br>   <br><br>* Processing result<br><br>   ```Python```<br>```   aGVsbG8=```<br>```   ```<br>    |
|b64dec |The b64dec function decodes the specified string from Base64. Syntax format:<br><br>```Python```<br>```b64dec(string)```<br> |* function example<br><br>   ```Python```<br>```   b64dec("aGVsbG8=")```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   hello```<br>```   ```<br>    |
|b32enc |b32enc function encodes the specified string in Base32. syntax format is as follows:<br><br>```Python```<br>```b32enc(string)```<br> |* function example<br><br>   ```Python```<br>```   b32enc("hello")```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   NBSWY3DP```<br>```   ```<br>    |
|b32dec |The b32dec function decodes the specified string from Base32. The syntax is as follows:<br><br>```Python```<br>```b32dec(string)```<br> |* function example<br><br>   ```Python```<br>```   b32dec("NBSWY3DP")```<br>```   ```<br>   <br><br>* processing result<br><br>   ```Python```<br>```   hello```<br>```   ```<br>    |


<span id="87d788f4"></span>
## Function examples

<span id="265f79f2"></span>
### Example 1: Extract `QueryLog` content.


* `QueryLog` content example

   ```JSON
   [
     [
       {
         "double_key": 1.1,
         "name": "bytedance",
         "obj_key": {
           "key1": 1,
           "key2": "key2",
           "key_double": 1.1,
           "key_long": 123
         },
         "type": 1
       }
     ]
   ]
   ```
   

* function examples

   
   |comparison items |without using function |use toPrettyJson function |
   |---|---|---|
   |Notification content configuration |`{{QueryLog}}` |`{{toPrettyJson(QueryLog)}}` |
   |result |```JSON```<br>```<[][]map[string]interface {} Value>```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">no actual value output.</div><br> |```JSON```<br>```[```<br>```  [```<br>```    {```<br>```      "double_key": 1.1,```<br>```      "name": "bytedance",```<br>```      "obj_key": {```<br>```        "key1": 1,```<br>```        "key2": "key2",```<br>```        "key_double": 1.1,```<br>```        "key_long": 123```<br>```      },```<br>```      "type": 1```<br>```    }```<br>```  ]```<br>```]```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The actual value has been output.</div><br> |
   


<span id="a7b368a1"></span>
### Example 2: Get the first 35 characters from the execution info page link


* Content example of `{{DetailUrl}}`

   ```Python
   https://console.byteplus.com/tls/region:tls+cn-beijing/project/a573686e-d097-4227-9fa5-612d0ae2****/alarms/7070267f-30da-4861-8d0a-01f4bc6d5****detail
   ```
   

* Function example

   ```Python
   {{substr(0,68, DetailUrl)}}
   ```
   

* Processing result

   ```Python
   https://console.byteplus.com/tls/
   ```
   


<span id="3c0596d9"></span>
### Example 3: Convert the start timestamp of the last execution statement in the alarm to the specified format


* Content example of `{{NotifyTimeUnix}}`

   ```Python
   1708582822
   ```
   

* Function example

   ```Python
   Start time of the last executed statement in this alarm: {{date("2006-01-02 15:04:05",QueryStartTime)}}
   ```
   

* Processing result

   ```Python
   Start time of the last executed statement in this alarm: 2024-02-22 14:20:22
   ```
   


<span id="6093e53d"></span>
### Example 4: Perform SHA256 encryption on the alarm policy ID


* Content example of `{{AlarmID}}`

   ```Python
   0a335663-88f1-4b51-ad67-c71ae008****
   ```
   

* Function example

   ```Python
   Alarm policy ID: {{sha256sum(AlarmID)}}
   ```
   

* Processing result

   ```Python
   Alarm policy ID: b8dc90d8de9cc33efffab28ad263598de8938f09356f83632176bff09ef6****
   ```
