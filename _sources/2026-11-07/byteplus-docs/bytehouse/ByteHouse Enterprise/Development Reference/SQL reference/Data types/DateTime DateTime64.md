---
title: "DateTime DateTime64"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/datetime-datetime64"
---

<span id="aa823169"></span>
# DataTime
Timestamp type. Stores Unix timestamps using four bytes (unsigned). Allows values within the same range as the date type. The minimum value is 1970-01-01 00:00:00. Timestamp values are accurate to the second (no leap seconds).
Value range: [1970-01-01 00:00:00, 2106-02-07 06:28:15].
<span id="时区 {#shi-qu}"></span>
## Timezone
Uses the system timezone of the client or server at launch, converting timestamps from text (broken into components) to binary and back. Information about daylight saving time will be lost in the text format.
By default, when the client connects to the service, it uses the server's timezone. You can set to use the client timezone by activating the client command line option `--use_client_time_zone`.
Therefore, when dealing with text dates (for example, when saving text dumps), remember that there might be ambiguities during the changes in daylight saving time, and there could be problems matching the data if the timezone changes.
<span id="a6c0fbf9"></span>
# DateTime64
This type allows storing a moment in time as date plus time, with defined sub-second accuracy.
Time scale size (precision): 10-precision seconds
Syntax:
```sql
DateTime64(precision, [timezone])
```

Internally, this type stores data as Int64 type ticks since the start of the Linux epoch (1970-01-01 00:00:00UTC). The resolution of time scales is determined by the precision parameter. `DateTime64` Type can store timezone information just like it stores other data columns. The timezone affects how the `DateTime64` Type values are displayed in text format, as well as how time data specified in the string form ('2020-01-01 05:00:01.000') is parsed. The timezone is not stored in the rows of the table (nor in the resultset) but is stored in the column's metadata. For more details, please refer to the DateTime Data Type.
The value range: [1900-01-01 00:00:00, 2299-12-31 23:59:59.99999999] (Note: The maximum is precision 8).
<span id="0a6b498e"></span>
## Example
**1.** Create a table with a `DateTime64` type column and insert data into it:
```sql
CREATE TABLE dt
(
    `timestamp` DateTime64(3, 'Asia/Istanbul'),
    `event_id` UInt8
)
ENGINE = TinyLog
```

```sql
INSERT INTO dt Values (1546300800000, 1), ('2019-01-01 00:00:00', 2)
```

```sql
SELECT * FROM dt
```

```text
┌───────────────timestamp─┬─event_id─┐
│ 2019-01-01 03:00:00.000 │        1 │
│ 2019-01-01 00:00:00.000 │        2 │
└─────────────────────────┴──────────┘
```

When inserting a date-time as an integer type, it is considered a Unix timestamp (UTC) scaled appropriately. `1546300800000` (Precision of 3) represents `'2019-01-01 00:00:00'` UTC. However, since the `Timestamp` column specifies the `Asia/Istanbul` (UTC+3) timezone, it is displayed as `'2019-01-01 03:00:00'` when output as a string.
When inserting a string as a datetime, it will be assigned timezone information. `'2019-01-01 00:00:00'` will be considered to be in the `Asia/Istanbul` timezone and stored as `1546290000000`.
**2.** Filter values of `DateTime64` type
```sql
SELECT * FROM dt WHERE timestamp = toDateTime64('2019-01-01 00:00:00', 3, 'Asia/Istanbul')
```

```text
┌───────────────timestamp─┬─event_id─┐
│ 2019-01-01 00:00:00.000 │        2 │
└─────────────────────────┴──────────┘
```

Unlike `DateTime`, values of `DateTime64` type are not automatically converted from `String` type values
**3.** Get timezone information of `DateTime64` type values:
```sql
SELECT toDateTime64(now(), 3, 'Asia/Istanbul') AS column, toTypeName(column) AS x
```

```text
┌──────────────────column─┬─x──────────────────────────────┐
│ 2019-10-16 04:12:04.000 │ DateTime64(3, 'Asia/Istanbul') │
└─────────────────────────┴────────────────────────────────┘
```

**4.** Timezone conversion
```sql
SELECT
toDateTime64(timestamp, 3, 'Europe/London') as lon_time,
toDateTime64(timestamp, 3, 'Asia/Istanbul') as mos_time
FROM dt
```

```text
┌───────────────lon_time──┬────────────────mos_time─┐
│ 2019-01-01 00:00:00.000 │ 2019-01-01 03:00:00.000 │
│ 2018-12-31 21:00:00.000 │ 2019-01-01 00:00:00.000 │
└─────────────────────────┴─────────────────────────┘
```
