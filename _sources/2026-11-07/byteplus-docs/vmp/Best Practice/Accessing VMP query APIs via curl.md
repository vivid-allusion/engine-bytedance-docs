---
title: "Accessing VMP query APIs via curl"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Accessing_VMP_query_APIs_via_curl"
---

This topic provides complete, ready\-to\-run curl examples and is intended for users who need to access VMP workspaces via curl. This access method supports BasicAuth authentication. This topic details access methods for the query APIs, covering instant queries, range queries, time series queries, and label key/value queries. Applicable scenarios include API integration testing, script integration, and O&M troubleshooting.

<span id="5r0fe0vD"></span>
## Prerequisites

Before you make calls, prepare the following information:


* A VMP workspace and its **query URL (query_url)** . For details on obtaining query URLs, see [Obtaining workspace URLs](https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL?lang=en).

* BasicAuth username/password **:**  The BasicAuth account and password configured on the workspace details page. These credentials will be used for BasicAuth authentication to access the workspace.

* Dependencies and environment variables:

   
   |**Dependency** |**Purpose** |**Required** |
   |---|---|---|
   |curl |Sends HTTP requests |Yes |
   |base64 |Serves as a tool for manually constructing a BasicAuth request header |No |
   |jq |Formats JSON responses for readability |No |
   

   Configure environment variables in Shell:

   ```Bash
   export VMP_QUERY_URL="https://your-vmp-query-endpoint"
   export VMP_USERNAME="your_basic_auth_username"
   export VMP_PASSWORD="your_basic_auth_password"
   ```
   


<span id="Qcqg9uNl"></span>
## Query examples

<span id="iaSRN9d3"></span>
### API descriptions and call examples


|**API path** |**Typical purpose** |**Description** |
|---|---|---|
|/api/v1/query |Instant query |Queries the current value at a specific time point. |
|/api/v1/query_range |Range queries |Queries data within a specified time period to reflect trends. |
|/api/v1/series |Queries matching time series |Suitable for confirming whether a metric or label combination exists. |
|/api/v1/labels |Queries label keys |Suitable for querying available labels in the current workspace. |
|/api/v1/label/<name\>/values |Queries label values |Suitable for querying the set of existing values for a specific label key. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Key fields in responses to API calls are described as follows:</div>



* <div data-tips="true" data-tips-type="default">status: Indicates whether the request is successful.</div>


* <div data-tips="true" data-tips-type="default">data.resultType: Indicates the result type.</div>


* <div data-tips="true" data-tips-type="default">data.result: Contains the actual metric query result.</div>



<span id="ndbuEYHO"></span>
### Instant queries

```Bash
# "query" is the query statement. Replace it with your actual PromQL statement based on your scenario.
# "time" specifies the query time and can be adjusted to fit your actual scenario. It is either a timestamp in seconds or in RFC3339 format.
curl --location --user "$VMP_USERNAME:$VMP_PASSWORD" \
  --get "$VMP_QUERY_URL/api/v1/query" \
  --data-urlencode 'query=sum(up)' \
  --data-urlencode "time=$(date +%s)" | jq
```


<span id="AbzspiU7"></span>
### Range queries

```Bash
# "query" is the query statement. Replace it with your actual PromQL statement based on your scenario.
# "start" and "end" define the query time range and can be adjusted to fit your actual scenario. The value is a timestamp in seconds or in RFC3339 format.
# "step" specifies the query interval and can be configured based on your actual scenario. The format is a time duration, for example, 60s.
curl --location --user "$VMP_USERNAME:$VMP_PASSWORD" \
  --get "$VMP_QUERY_URL/api/v1/query_range" \
  --data-urlencode 'query=rate(prometheus_http_requests_total[5m])' \
  --data-urlencode 'start=2025-10-09T07:25:00Z' \
  --data-urlencode 'end=2025-10-09T07:55:00Z' \
  --data-urlencode 'step=60s' | jq
```


<span id="MMyFCCo9"></span>
### Time series queries

```Bash
# "match[]" specifies the range of time series to match and can be adjusted to fit your actual scenario. It follows the standard series selector syntax.
# "start" and "end" define the query time range and can be adjusted to fit your actual scenario. The value is a timestamp in seconds or in RFC3339 format.
curl --location --user "$VMP_USERNAME:$VMP_PASSWORD" \
  --get "$VMP_QUERY_URL/api/v1/series" \
  --data-urlencode 'match[]=up' \
  --data-urlencode 'start=2025-10-09T06:55:00Z' \
  --data-urlencode 'end=2025-10-09T07:55:00Z' | jq
```


<span id="Uidqn92I"></span>
### Label key queries

```Bash
# "match[]" specifies the range of time series to match and can be adjusted to fit your actual scenario. It follows the standard series selector syntax.
# "start" and "end" define the query time range and can be adjusted to fit your actual scenario. The value is a timestamp in seconds or in RFC3339 format.
curl --location --user "$VMP_USERNAME:$VMP_PASSWORD" \
  --get "$VMP_QUERY_URL/api/v1/labels" \
  --data-urlencode 'match[]=up' \
  --data-urlencode 'start=2025-10-09T06:55:00Z' \
  --data-urlencode 'end=2025-10-09T07:55:00Z' | jq
```


<span id="U1OjpqDX"></span>
### Label value queries

```Bash
# You can specify a label based on your scenario. This example queries all values of the "instance" label key.
curl --location --user "$VMP_USERNAME:$VMP_PASSWORD" \
  --get "$VMP_QUERY_URL/api/v1/label/instance/values" | jq
```


<span id="sqKJc84m"></span>
## FAQ and troubleshooting suggestions

<span id="Dy93Ezwa"></span>
### Q1: Why does authentication fail with the 401 or 403 error?

**Possible causes:** 


* The BasicAuth username or password is incorrect.

* The requested workspace URL is invalid.

* The current account lacks access permission for the target workspace.


**Troubleshooting suggestions:** 


* Use a query command to verify connectivity.

* Confirm whether the credentials in `--user "$VMP_USERNAME:$VMP_PASSWORD"` are correct.


<span id="JPnOKShX"></span>
### Q2: Why do queries succeed but return empty results?

**Possible causes:** 


* The PromQL query did not match any data.

* The query time range is too narrow.

* Written metric data has not been synchronized to the query side.


**Troubleshooting suggestions:** 


* Use a simpler metric name.

* Expand the time range (for example, from the last 5 minutes to the last 30 minutes).

* Wait 5 to 10 minutes and then retry the query.


<span id="C8M2tuLD"></span>
### Q3: Why is the command output unreadable despite successful execution?

**Possible causes:** 


* The results are returned as compressed single\-line JSON.

* The jq tool has not been installed on the local system, so the output cannot be formatted.


**Troubleshooting suggestions:** 


* Add `| jq` to the end of the command.

* If the jq tool is not installed locally, temporarily remove this command and install the tool after confirming the API is available.
