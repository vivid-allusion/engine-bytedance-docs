---
title: "Input⧸Output formats"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/input-output-formats"
---

ByteHouse can accept and return data in various formats. Supported input formats can be submitted to `INSERT` statements, run `SELECT` statements from file tables (File, URL, HDFS, or external directories), and supported output formats can format the results of `SELECT` statements, or write to file tables via `INSERT`.

Here are the supported formats:


|Format |Input |Output |
|---|---|---|
|TabSeparated |✔ |✔ |
|TabSeparatedRaw |✔ |✔ |
|TabSeparatedWithNames |✔ |✔ |
|TabSeparatedWithNamesAndTypes |✔ |✔ |
|Template |✔ |✔ |
|TemplateIgnoreSpaces |✔ |✗ |
|CSV |✔ |✔ |
|CSVWithNames |✔ |✔ |
|CustomSeparated |✔ |✔ |
|Values |✔ |✔ |
|Vertical |✗ |✔ |
|JSON |✗ |✔ |
|JSONAsString |✔ |✗ |
|JSONStrings |✗ |✔ |
|JSONCompact |✗ |✔ |
|JSONCompactStrings |✗ |✔ |
|JSONEachRow |✔ |✔ |
|JSONEachRowWithProgress |✗ |✔ |
|JSONStringsEachRow |✔ |✔ |
|JSONStringsEachRowWithProgress |✗ |✔ |
|JSONCompactEachRow |✔ |✔ |
|JSONCompactEachRowWithNamesAndTypes |✔ |✔ |
|JSONCompactStringsEachRow |✔ |✔ |
|JSONCompactStringsEachRowWithNamesAndTypes |✔ |✔ |
|TSKV |✔ |✔ |
|Pretty |✗ |✔ |
|PrettyCompact |✗ |✔ |
|PrettyCompactMonoBlock |✗ |✔ |
|PrettyNoEscapes |✗ |✔ |
|PrettySpace |✗ |✔ |
|Protobuf |✔ |✔ |
|ProtobufSingle |✔ |✔ |
|Avro |✔ |✔ |
|AvroConfluent |✔ |✗ |
|Parquet |✔ |✔ |
|Arrow |✔ |✔ |
|ArrowStream |✔ |✔ |
|ORC |✔ |✔ |
|RowBinary |✔ |✔ |
|RowBinaryWithNamesAndTypes |✔ |✔ |
|Native |✔ |✔ |
|Null |✗ |✔ |
|XML |✗ |✔ |
|CapnProto |✔ |✗ |
|LineAsString |✔ |✗ |
|Regexp |✔ |✗ |
|RawBLOB |✔ |✔ |
