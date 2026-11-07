---
title: "Arithmetic operation syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Arithmetic-operation-syntax-2"
---

This topic describes the arithmetic operation syntax supported by Torch Log Service (TLS) and offers examples on how to use the syntax.

<span id="Syntax description"></span>
## Syntax description

TLS offers common arithmetic operation and analysis syntax based on the arithmetic operation syntax. The following table describes the supported arithmetic operators.


|Operator |Description |
|---|---|
|`+` |The addition operator that adds two operands. |
|`-` |The subtraction operator that subtracts the right\-side operand from the left\-side operand. |
|`*` |The multiplication operator that multiplies two operands. |
|`/` |The division operator that divides the left\-side operand by the right\-side operand.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When using the / operator, if both the dividend and the divisor are integers, the result will only keep the integer part and discard the decimal part. You can use <code>a * 1.0... / b</code> operation to retain the decimal part. For example, <code>SELECT 10 / 3</code> results in 3, while <code>SELECT 10 * 1.00 / 3</code> results in 3.33.</div><br> |
|`%` |The modulo operator that returns a remainder after the left\-side operand is divided by the right\-side operand. |


<span id="e67e9767"></span>
## Examples


|Function |Description |Sample SQL Statement |
|---|---|---|
|`+` |Returns the sum of a and b. |<PreCode lang="sql" text={`* \| select a + b`}\> |
|`-` |Returns the difference of a and b. |<PreCode lang="sql" text={`* \| select a - b`}\> |
|`*` |Returns the product of a and b. |<PreCode lang="sql" text={`* \| select a * b`}\> |
|`/` |Returns the quotient of a and b. |<PreCode lang="sql" text={`* \| select a / b`}\> |
|`%` |Returns the remainder after a is divided by b. |<PreCode lang="sql" text={`* \| select a % b`}\> |
