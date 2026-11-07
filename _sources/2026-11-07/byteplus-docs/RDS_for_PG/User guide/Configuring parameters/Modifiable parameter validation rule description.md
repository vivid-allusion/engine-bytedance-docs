---
title: "Modifiable parameter validation rule description"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Modifiable_parameter_validation_rule_description"
---

The range of values and data types of different parameters are different, and different verification rules need to be met when modifying them.


* Single selection

   * Value range format: [a | b |... | n]

   * Data types are typically bool, enum, or string.

   * Example

      The parameter log_connections is of type bool and has a value range of [on | off], which can be modified to either on or off.

* Multiple selection

   * Value range format: [\* a | b]

   * Data type is typically string.

   * Example

      Parameter shared_preload_libraries is of type string and the range is [\* auth_delay | pg_stat_statements | auto_explain | pgaudit | pgnodemx]. This parameter


can be modified as a combination of at least one of the above optional values, for example: auth_delay or auth_delay, pgaudit or auto_explain, pgaudit.


* Range validation

   * Value range format: [a, b\-c] or [a\-b]

   * The data type is either general integer or real.

   * Example

      * Parameter checkpoint_completion_target is of type real in the range [0\-1], and can be modified to any floating\-point number in the range 0 to 1.

      * Parameter autovacuum_vacuum_cost_delay type is integer, the range is [0\-50], the parameter can be modified to any integer in the range of 0 to 50.

      * Parameter temp_file_limit is of type integer in the range [\-1,2097152\-instance storage \* 80%], which can be set to \-1, or any integer value between [2097152~ instance storage \* 80%].

* No validation rule

   * Value range format: [\*]

   * Data type is typically string.
