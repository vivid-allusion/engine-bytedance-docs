---
title: "Basic syntax"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Basic-syntax"
---

<span id=".5Y-C5pWw"></span>
## Argument

Use an equal sign to assign a value or expression to a specified argument name; the argument name can consist of letters, numbers, underscores (_) and hyphens (\-), but the first character cannot be a number. Example: `Name = "tfecs"`.

<span id=".5Z2X"></span>
## Block

A structure composed of multiple arguments that also supports nesting. A block consists of a block type, block tags, and block body. Example:

```Plain Text
resource "instance" "myinstance" {
    name   = "tfecs"
    ......
    network {
        id = "subnet-3tispp1nai4e8i4q****"
    }
}
```



* Block Type: To define a block body, a block type must first be defined. In this example, `resource` and `network` are block types, where `resource` is the top\-level block type and `network` is the nested block type.

* Block Tag: Defined after the block type. In this example, `resource` contains two tags, `instance` and `myinstance`, while `network` does not have any block tags.

* Block body: Define a block body in the last part and encapsulate it in braces ( { } ). You can nest blocks of other types in the block body for different hierarchies.


<span id=".5Y-C5pWw57G75Z6L"></span>
## Argument type

<span id=".5Z-65pys57G75Z6L"></span>
### Primitive types

A primitive type is a simple type that does not consist of any other types.


* string: A string consists of one or multiple Unicode characters, such as "hello."

* number: A number can be an integer or a decimal.

* bool: A bool value can be true or false.


Example:

```Plain Text
ZoneId       = "cn-beijing-a"
Count        = 1
UniqueSuffix = true
```


<span id=".5aSN5ZCI57G75Z6L"></span>
### Complex types

A complex type consists of a group of values.


* list(...): A list is a collection of values of the same data type that start from zero. The data type can be a primitive type or block.

   * Format: Use `[]` to encapsulate.

   * Example:

   ```Plain Text
   InstanceIds = [
     "i-3tigy72q3u3vj0x2****"
     "i-3tigy72q3u3vj0x2****"
   ]
   ```
   

* map(...): A map is a collection of elements in the form of key\-value pairs. A key must be a string, and a value must be a string, number, or bool. Additionally, all values in a map must be of the same type.

   * Format: Use `{}` encapsulate, with keys and values separated by`:`or`=`connections, and key\-value pairs separated by line break or comma.

   * Example:

   ```Plain Text
   ResponseMetadata = {
     "RequestId": "xxxxxxxxxx"
     "Action": "StartInstance"
   }
   ```
   

* set(...): A set is a type similar to list elements, using `[]` to encapsulate, but its data must be unique.


<span id=".54m55q6K57G75Z6L"></span>
### Special types


* null: Empty type, if an argument is set to null, it indicates that this argument is not provided. Terraform will automatically ignore this argument and use the default value.


<span id=".5rOo6YeK"></span>
## Comment


* # or //: Insert one of them at the beginning of a line to comment out the line.

* /*And*/\*: Multi\-line comments start with /\* and end with \*/, the content in between is the comment.
