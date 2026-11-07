---
title: "What if you encounter the error described in this topic when performing data synchronization from MySQL to ElasticSearch?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/What_if_you_encounter_the_error_described_in_this_topic_when_performing_"
---

**Description**: When you encounter the following error while performing data synchronization from MySQL to ElasticSearch, you can troubleshoot the problem according to the solutions described in this topic.

```json
{
  "_index": "my-dts-index",
  "_type": "_doc",
  "_id": "20744",
  "status": 400,
  "error": {
    "type": "mapper_parsing_exception",
    "reason": "failed to parse field [update_time] of type [date] in document with id '20744'",
    "caused_by": {
      "reason": "Invalid format: \"2019-08-22 11:08:55\" is malformed at \" 11:08:55\"",
      "type": "illegal_argument_exception"
    }
  }
}
```


**Possible cause**: The format of the date field `update_time` of the `my-dts-index`  index does not match the expected format of ElasticSearch.

Since the MySQL date field `update_time` is set to `2019-08-22 11:08:55`, and the date format expected by ElasticSearch is `11:08:55`, the MySQL date format is inconsistent with the ElasticSearch time format, which causes the data synchronization {"Data synchronization"} {"Task"} to report an error.

**Solution**: Ensure that the MySQL date format meets the expected format of ElasticSearch. Configure the correct time format mapping during the structural migration stage of the task, or directly modify the ElasticSearch mapping date format. The time formats supported by the default DTS structure mapping are as follows:


* `strict_date_optional_time`

* `yyyy-MM-dd HH:mm:ss`

* `yyyy-MM-dd`

* `HH:mm:ss`

* `epoch_millis`

* `yyyy-MM-dd HH:mm:ss.SSS`
