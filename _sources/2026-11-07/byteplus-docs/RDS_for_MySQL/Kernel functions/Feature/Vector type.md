---
title: "Vector type"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Vector_type"
---

This topic describes the vector retrieval feature of RDS for MySQL.

<span id="rYdebcTY"></span>
## Supported version


* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20250815 and above.

* MySQL 8.4, with a kernel minor version of MySQL 8.4.7_20260415 or later.


<span id="aQ0qkoK9"></span>
## Background

With the rapid development of artificial intelligence and machine learning technologies, vector data is playing an increasingly important role in various intelligent application scenarios. In AI application fields such as image recognition, natural language processing, and recommendation systems, unstructured data (such as images, text, and audio) must be converted into high\-dimensional vectors for storage and retrieval. Traditional databases lack support for native vector data types, and developers can only use TEXT or BLOB types to store the string representation of vectors. This method has poor storage efficiency and does not allow for efficient vector operations.

RDS for MySQL provides a solution for storing vector data by introducing the native VECTOR data type of MySQL 9.0.


* **Native vector storage**: The VECTOR type uses 4\-byte single\-precision floating\-point numbers to store each dimension of a vector and supports vector data with 1 to 16,383 dimensions.

* **SQL standard compatibility**: Fully compatible with standard SQL syntax, allowing developers to use familiar SQL statements to add, delete, modify, and query vector data.


<span id="TC8RUJBL"></span>
## Feature introduction

<span id="NCSK3amk"></span>
### VECTOR data type

The VECTOR data type stores vector data with fixed dimensions:


|**Syntax** |**Description** |**Dimension range** |**Storage format** |
|---|---|---|---|
|`VECTOR(N)` |N\-dimensional vector type |1~16383 |4\-byte single\-precision floating\-point number |


<span id="PBct7fYq"></span>
### Basic vector functions


|**Function name** |**Syntax** |**Description** |**Sample** |
|---|---|---|---|
|`TO_VECTOR/ STRING_TO_VECTOR` |`TO_VECTOR(text)`<br><br>`STRING_TO_VECTOR(text)` |Convert a string to a vector type |`TO_VECTOR('[1,2,3,4]')`<br><br>`STRING_TO_VECTOR('[1,2,3,4]')` |
|`FROM_VECTOR/ VECTOR_TO_STRING` |`FROM_VECTOR(vector)`<br><br>`VECTOR_TO_STRING(vector)` |Convert a vector type to a readable hex string<br><br> |`FROM_VECTOR(vector_column)`<br><br>`VECTOR_TO_STRING(vector_column)` |
|`VECTOR_DIM` |`VECTOR_DIM(vector)` |Obtain the dimension of the vector |`VECTOR_DIM('[1,2,3,4]')` |


<span id="4T799gjc"></span>
### Vector math functions


|Function name |Syntax |Description |
|---|---|---|
|`VECTOR_NORM` |`VECTOR_NORM(vector)` |Calculate the L2 norm (Euclidean length) of a vector |
|`VECTOR_NORMALIZE` |`VECTOR_NORMALIZE(vector)` |Vector normalization to a length of 1 |
|`VECTOR_ADD` |`VECTOR_ADD(vector1, vector2, ...)` |Vector element\-wise addition |
|`VECTOR_SUB` |`VECTOR_SUB(vector1, vector2, ...)` |Element\-wise vector subtraction |
|`VECTOR_MUL` |`VECTOR_MUL(vector1, vector2, ...)` |Vector element\-wise multiplication (Hadamard product) |


<span id="MUGDkKNw"></span>
### Vector distance calculation functions


|Function name |Syntax |Description |
|---|---|---|
|`L1_DISTANCE` |`L1_DISTANCE(vector1, vector2)` |Manhattan distance |
|`L2_DISTANCE/ EUCLIDEAN_DISTANCE` |`L2_DISTANCE(vector1, vector2)`<br><br>`EUCLIDEAN_DISTANCE(vector1, vector2)` |Euclidean distance |
|`L2_SQUARED_DISTANCE` |`L2_SQUARED_DISTANCE(vector1, vector2)` |Squared Euclidean distance |
|`COSINE_DISTANCE` |`COSINE_DISTANCE(vector1, vector2)` |Cosine distance |
|`INNER_PRODUCT` |`INNER_PRODUCT(vector1, vector2)` |Inner product (dot product) |
|`NEGATIVE_INNER_PRODUCT` |`NEGATIVE_INNER_PRODUCT(vector1, vector2)` |Negative inner product |
|`SPHERICAL_DISTANCE` |`SPHERICAL_DISTANCE(vector1, vector2)` |Spherical distance<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This function requires the input parameter to be a unit vector. Otherwise, the result is 0. Normalize the vector using the <code>VECTOR_NORMALIZE</code> function before use.</div><br> |


<span id="y8Erdmkm"></span>
## Instructions and examples

<span id="DR6QM94m"></span>
### Basic vector operations


* **Create a table with vector columns**

   ```SQL
   -- Create a product feature table to store 4-dimensional product vector features
   CREATE TABLE product_features (
       product_id INT PRIMARY KEY,
       product_name VARCHAR(255),
       category VARCHAR(100),
       feature_vector VECTOR(4),
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   ) ENGINE=InnoDB;
   ```
   

* **Insert vector data**

   ```SQL
   -- Insert product vector data
   INSERT INTO product_features (product_id, product_name, category, feature_vector) 
   VALUES 
   (1, '手机', '电子产品', TO_VECTOR('[0.1, 0.2, 0.3, 0.4]')),
   (2, '手机', '电子产品', TO_VECTOR('[0.15, 0.25, 0.28, 0.38]')),
   (3, '手机', '电子产品', TO_VECTOR('[0.12, 0.22, 0.32, 0.42]'));
   ```
   

* **Query and display vector data**

   ```SQL
   -- Query vector data (in a readable format)
   SELECT 
       product_id,
       product_name,
       FROM_VECTOR(feature_vector) AS readable_vector
   FROM product_features 
   WHERE product_id = 1;
   ```
   

   The following is a sample response:

   ```SQL
   +------------+--------------+---------------------------------------------------+
   | product_id | product_name | readable_vector                                   |
   +------------+--------------+---------------------------------------------------+
   |          1 | 手机         | [1.00000e-01,2.00000e-01,3.00000e-01,4.00000e-01] |
   +------------+--------------+---------------------------------------------------+
   ```
   


<span id="vubAciJG"></span>
### Vector mathematical operations


* **Vector normalization**

   ```SQL
   -- Normalize the product feature vector
   SELECT 
       product_id,
       product_name,
       VECTOR_NORM(feature_vector) AS original_norm,
       FROM_VECTOR(VECTOR_NORMALIZE(feature_vector)) AS normalized_vector
   FROM product_features;
   ```
   

   The following is a sample response:

   ```SQL
   +------------+--------------+--------------------+---------------------------------------------------+
   | product_id | product_name | original_norm      | normalized_vector                                 |
   +------------+--------------+--------------------+---------------------------------------------------+
   |          1 | 手机         | 0.5477225697477194 | [1.82574e-01,3.65148e-01,5.47723e-01,7.30297e-01] |
   |          2 | 手机         | 0.5547972592143449 | [2.70369e-01,4.50615e-01,5.04689e-01,6.84935e-01] |
   |          3 | 手机         | 0.5844655535095068 | [2.05316e-01,3.76412e-01,5.47509e-01,7.18605e-01] |
   +------------+--------------+--------------------+---------------------------------------------------+
   ```
   


<span id="WCxcAiZk"></span>
### Similarity search


* **Product recommendation based on cosine similarity**

   ```SQL
   -- Find the 5 products most similar to the specified product
   SET @target_vector = (SELECT feature_vector FROM product_features WHERE product_id = 1);
   
   SELECT 
       p.product_id,
       p.product_name,
       p.category,
       COSINE_DISTANCE(p.feature_vector, @target_vector) AS similarity_score
   FROM product_features p
   WHERE p.product_id != 1
   ORDER BY similarity_score ASC
   LIMIT 5;
   ```
   

   The returned example is as follows:

   ```SQL
   +------------+--------------+--------------+------------------------+
   | product_id | product_name | category     | similarity_score       |
   +------------+--------------+--------------+------------------------+
   |          3 | 手机         | 电子产品       | 0.00039043972636043645 |
   |          2 | 手机         | 电子产品       |   0.009461057988503607 |
   +------------+--------------+--------------+------------------------+
   ```
   

* **Nearest neighbor search based on euclidean distance**

   ```SQL
   -- Find the product closest to the target vector
   SELECT 
       product_id,
       product_name,
       L2_DISTANCE(feature_vector, TO_VECTOR('[0.1, 0.2, 0.3, 0.4]')) AS distance
   FROM product_features
   ORDER BY distance ASC
   LIMIT 10;
   ```
   

   The returned example is as follows:

   ```SQL
   +------------+--------------+----------------------+
   | product_id | product_name | distance             |
   +------------+--------------+----------------------+
   |          1 | 手机         |                    0 |
   |          3 | 手机         | 0.039999976211686064 |
   |          2 | 手机         |  0.07615773363159213 |
   +------------+--------------+----------------------+
   ```
   


<span id="gnLjLm9j"></span>
### Vector aggregation analysis


* **Vector similarity matrix calculation**

   ```SQL
   -- Calculate the similarity matrix between all products
   SELECT 
       p1.product_id AS product1_id,
       p1.product_name AS product1_name,
       p2.product_id AS product2_id,
       p2.product_name AS product2_name,
       COSINE_DISTANCE(p1.feature_vector, p2.feature_vector) AS cosine_similarity,
       L2_DISTANCE(p1.feature_vector, p2.feature_vector) AS euclidean_distance
   FROM product_features p1
   CROSS JOIN product_features p2
   WHERE p1.product_id < p2.product_id
   ORDER BY cosine_similarity ASC;
   ```
   

   The returned example is as follows:

   ```SQL
   +-------------+---------------+-------------+---------------+------------------------+----------------------+
   | product1_id | product1_name | product2_id | product2_name | cosine_similarity      | euclidean_distance   |
   +-------------+---------------+-------------+---------------+------------------------+----------------------+
   |           1 | 手机          |           3 | 手机          | 0.00039043972636043645 | 0.039999976211686064 |
   |           2 | 手机          |           3 | 手机          |   0.006352599451149077 |  0.07071067074295588 |
   |           1 | 手机          |           2 | 手机          |   0.009461057988503607 |  0.07615773363159213 |
   +-------------+---------------+-------------+---------------+------------------------+----------------------+
   ```
   


<span id="nbGf4cAi"></span>
### Precautions


* The current version does not support using VECTOR columns as primary keys, foreign keys, unique keys, or partition keys.

* VECTOR columns cannot be used as sources for histograms.

* The VECTOR type only supports equality comparisons (`=`, `!=`) and does not support size comparisons (`>`, `<`, `>=`, `<=`).

* The following functions support or do not support the VECTOR type:

   * VECTOR values can be used with the MySQL string functions `BIT_LENGTH`, `CHAR_LENGTH`, `HEX`, `LENGTH`, and `TO_BASE64`. Other string functions do not accept the VECTOR type as a parameter.

   * VECTOR can be used as a parameter for the encryption functions `AES_ENCRYPT`, `COMPRESS`, `MD5`, `SHA1`, and `SHA2`. Other encryption functions do not support VECTOR type parameters.

   * VECTOR can be used as a parameter for the CASE operator and related flow control functions, such as `COALESCE`, `IFNULL`, `NULLIF`, and `IF`.

   * VECTOR can be used as a parameter for CAST (expression AS BINARY), and the result is a binary string with the same content as the VECTOR parameter. However, converting to VECTOR by using CAST is not supported. Alternatively, you can use `STRING_TO_VECTOR` / `TO_VECTOR` to convert a valid vector string to VECTOR.

   * The VECTOR data type cannot be used as a parameter for aggregate or window functions, except for `COUNT [DISTINCT]`.

* VECTOR cannot be used as a parameter for the following types of functions or operators:

   * Numeric functions and operators

   * Time functions

   * Full\-text search functions

   * XML functions

   * Bit functions (such as bitwise AND or bitwise OR)

   * JSON functions
