---
title: "Style conventions"
product: "Terraform"
product_code: "tf"
source: "https://docs.byteplus.com/en/docs/tf/Style-conventions"
---

Terraform has the following style conventions to ensure a consistent style across configuration files and modules written by different teams. We recommend that you follow these conventions.


* Indent two spaces for each nesting level.

* When single\-line arguments appear consecutively at the same nesting level, align their equal signs. For example,

   ```Plain Text
   Name           = "tfecs"
   InstanceType   = "ecs.g1.large"
   ```
   

* When a block body contains arguments and blocks, place all arguments at the top, put nested blocks below the arguments, and separate the arguments from the nested blocks with a blank line.

* Separate argument groups in a block with blank lines.

* When a block body contains metadata and arguments, place the metadata at the top or bottom and separate it from other arguments with a blank line.

* Separate top\-level blocks with blank lines.

* Place nested blocks of the same type consecutively, and separate nested blocks of different types with blank lines.
