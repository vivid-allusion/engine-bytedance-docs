---
title: "HyperLogLog algorithm extension (postgresql-hll)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/postgresql"
---

<span id="a5z7lWe3"></span>
## Introduction

postgresql\-hll is a PostgreSQL extension based on the HyperLogLog algorithm. It introduces a custom data type `hll` to solve large\-scale data **cardinality estimation (count distinct)**  issues, such as billions or more, with minimal storage space and very fast computation speed.

<span id="1kJTHwzK"></span>
### Core advantages


* **Efficient storage and performance**: `hll` data objects require very small and fixed storage space (usually less than 16KB), which no longer increases linearly with the growth of raw data volume. It has an extremely fast calculation speed, typically completing within milliseconds.

* **Native aggregation capability**: it supports lossless merging (union) of `hll` objects at any dimension. For example, it can easily merge daily user visit records (DAU) into weekly (WAU) or monthly (MAU) unique user counts without rescanning the raw data.

* **Reliable estimation accuracy**: the default configuration achieves a standard error of about **0.8%** , balancing accuracy and resource consumption effectively. The extension also includes sparse and dense storage modes and can automatically switch based on data volume to optimize storage efficiency.


<span id="81HuuTs5"></span>
### Typical uses


* **Website/App activity statistics**: calculate key indicators such as daily active users (DAU) and monthly active users (MAU).

* **large\-scale deduplication counting**: count unique IP addresses in massive logs and the users visiting different products/contents.

* **Real\-time data analysis**: use its efficient merging features to perform sliding window analysis, such as calculating the rolling UV of the past 7 days.


<span id="CnbwjWH6"></span>
## Precautions

Before using the hll extension, understand and evaluate the following key limitations to avoid unexpected situations in production environments.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is a probabilistic data structure, not an exact storage.</div>



* **Imprecise calculation**

   hll provides an **estimated value** of cardinality, not an exact value. Although the error rate is low, it is essentially a probabilistic statistical model. Therefore, it is **strictly prohibited** to use it in any scenario requiring 100% accuracy, such as financial accounting, inventory management, and order counting.

* **Irreversible data**

   `hll` stores digest information after hashing the original data, making it impossible to restore any original values from it. For example, you cannot recover a specific list of user IDs from an `hll` object aggregating user IDs. It is only used for "counting," not for "tracing."

* **Strong extension dependency**

   If your data table contains `hll` columns, reading and writing to that table will strongly depend on the hll extension. **If this extension is uninstalled (** **`DROP EXTENSION hll;`**  **),**  all data in `hll` columns will become unreadable (appearing as garbled or errors), which is equivalent to data loss.

* **Hash function consistency**

   The merging (Union) of `hll` objects requires their hash configurations to be completely consistent. If you use hll in different systems or environments (for example, computing hash values on the Java server or aggregating in PostgreSQL), you must ensure that the **hash algorithm and seed used are the same** on both sides. Otherwise, the generated `hll` objects cannot be merged, and the calculated union result will be incorrect.

* **Data migration and synchronization risks**

   When using DTS (Data Transmission Service) or other tools for database migration, synchronization, or backups, you must ensure that the **target database instance has the hll extension installed in advance**. Otherwise, during data import, the `hll` data columns will cause migration failure or data corruption due to an unrecognized type.


<span id="dRiT3iE7"></span>
## Installation and uninstallation

<span id="3Vtp3S6h"></span>
### Install extension

In the database where the hll function is required, execute the following SQL command to **install** the extension.

```SQL
-- install hll extension
CREATE EXTENSION hll;
```


After successful installation, you can confirm it by querying the `pg_extension` system table.

```SQL
-- check whether the hll extension is installed
SELECT * FROM pg_extension WHERE extname = 'hll';
```


If the query returns results, the extension is installed and available for use.

<span id="1yARIwHi"></span>
### Uninstall extension

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Uninstalling the extension will disable all hll data columns, making the data unreadable. Before performing this operation, confirm that no business depends on hll data or that data migration is complete.</div>


If you are sure the hll extension is no longer needed, execute the following command to **uninstall**.

```SQL
-- uninstall hll extension
DROP EXTENSION hll;
```


<span id="rWiWfNTW"></span>
## Usage

The core workflow of the postgresql\-hll extension generally includes three steps:


1. **Hash**: convert the original values requiring distinct counting (e.g., user ID and IP address) to hash values using a hash function.

2. **Aggregate**: add these hash values into an `hll` data object for aggregation.

3. **Calculate**: estimate cardinality (distinct count) through the `hll` object, or merge multiple `hll` objects to compute the union.


<span id="L49vMf1k"></span>
### Hash and aggregation

hll extension does not directly process the original value but processes its hash values. The most common method is to combine the use of `hll_hash_*` series functions and the `hll_add_agg` aggregation function.

**Example: counting unique visitors (UV) by days**

Assuming we have a raw log table recording user access behaviors called `page_views`:

```SQL
CREATE TABLE page_views (
    log_time    TIMESTAMPTZ,
    user_id     TEXT
);
```


Now, we want to pre\-calculate daily UV data and store it in a result table called `daily_uniques`.


1. **Create a pre\-aggregation table**

   First, create a table for storing daily UV data, where the type of the `users` column is `hll`.

   ```SQL
   CREATE TABLE daily_uniques (
       stat_date   DATE PRIMARY KEY,
       users       HLL
   );
   ```
   

2. **Hash and aggregation data**

   Read data from the `page_views` table, and use `hll_hash_text` to convert `user_id` to hash values. Then, aggregate by day using `hll_add_agg` to generate `hll` objects, and insert into the `daily_uniques` table.

   ```SQL
   INSERT INTO daily_uniques(stat_date, users)
   SELECT
       DATE(log_time) AS stat_date,
       hll_add_agg(hll_hash_text(user_id)) AS users -- core actions
   FROM
       page_views
   GROUP BY
       stat_date;
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">hll provides various hash functions to support different data types, such as <code>hll_hash_bigint</code>, <code>hll_hash_int</code>, and <code>hll_hash_bytea</code>. Select the appropriate hash function based on your data type.   </div>
   

<span id="KBo37Dhw"></span>
### Cardinality estimation

After data is stored as `hll` type, you can use the `hll_cardinality` function to retrieve its estimated cardinality (i.e., the deduplicated quantity).

**Example: query the UV of a specific day**

```SQL
SELECT
    stat_date,
    hll_cardinality(users) AS estimated_uv
FROM
    daily_uniques
WHERE
    stat_date = '2026-02-12';
```


<span id="QAlDqACi"></span>
### Lossless merging

Lossless merging is one of postgresql\-hll’s most powerful features. You can merge `hll` objects stored in different rows (e.g., records from different dates) to calculate the deduplicated count over the entire time range without rescanning massive raw data.

**Example: calculate monthly active users (MAU)** 

Use the `hll_union_agg` function to merge all daily `hll` objects within a month into one, then calculate its total cardinality.

```SQL
SELECT
    EXTRACT(YEAR FROM stat_date) AS year,
    EXTRACT(MONTH FROM stat_date) AS month,
    -- merge the hll objects of all days in the month, then estimate the total cardinality
    hll_cardinality(hll_union_agg(users)) AS monthly_uv
FROM
    daily_uniques
WHERE
    stat_date >= '2026-01-01' AND stat_date < '2026-02-01'
GROUP BY
    year, month;
```


<span id="g7vBwv1k"></span>
### Sliding window analysis

Due to the high performance of `hll` merging, it is ideal for calculating metrics within a rolling time window, such as "rolling active users in the past 7 days".

**Example: calculating 7\-day rolling UV**

By combining window functions and `hll_union_agg`, sliding window calculations can be efficiently implemented.

```SQL
SELECT
    stat_date,
    hll_cardinality(
        hll_union_agg(users) OVER (
            ORDER BY stat_date
            ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
        )
    ) AS rolling_7day_uv
FROM
    daily_uniques
ORDER BY
    stat_date;
```


<span id="f89ud7VV"></span>
### Default configuration description

When creating an `hll` object, the extension uses a set of default parameters (e.g.,` log2m=11` and `regwidth=5`) that determine the precision and storage size of the `hll` object. In most scenarios, **the default configuration (with an error rate of about ±0.8%) already offers the best balance of performance and precision**, users do not need to adjust it manually.


* `hll_empty()`: this function creates an empty `hll` object based on the default **parameters**.

* `hll_add_agg(...)`: this aggregation function also creates an `hll` object using the **default parameters**.


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger"><code>hll</code> objects with different <strong>parameter</strong> configurations cannot be merged. To ensure data mergeability, it is strongly recommended to consistently use the unified default configuration throughout the database and avoid manually specifying different parameters during creation or aggregation.</div>


<span id="CxvJdEsb"></span>
## FAQs and troubleshooting


* **Q: Why is there a deviation between the hll calculation result and the accurate COUNT(DISTINCT ...) result?**  **A:**  This is normal. hll is a probabilistic data structure designed to trade minimal storage space for a sufficiently accurate estimate. It has inherent statistical error (about ±0.8% under the default configuration). If you need 100% accurate results, use the traditional COUNT(DISTINCT ...), but be prepared for significant computation and memory overhead.

* **Q: Why can't two ** **`hll`** ** objects be merged?**  **A:**  merge failure usually occurs because the internal configuration parameters of the two `hll` objects differ. For example, one `hll` object was created with a non\-default value of `log2m`, while the other used the default value. Make sure all `hll` objects involved in the merge share the same configuration. The simplest approach is to always use the default behavior of `hll_empty()` and `hll_add_agg` without manually specifying parameters.

* **Q: why ** **`hll`** ** data columns appear garbled or query errors?**  **A:**  The most common reason for this is that the hll extension is not installed or enabled in the current database connection. Execute `CREATE EXTENSION IF NOT EXISTS hll;` to ensure the extension is available. Another possibility is that the extension was accidentally uninstalled, which will cause data to be unrecoverable. Refer to the risks described in the "Precautions" section.

* **Q: after data migration (DTS), ** data in **`hll`** ** column is unusable. Why?**  **A:**  This usually occurs because the hll extension is not installed in the target database when importing data. The migration tool cannot recognize the `hll` type and may mistakenly import the data as ordinary binary data. Ensure the hll extension is installed in the target database before starting the migration task.
