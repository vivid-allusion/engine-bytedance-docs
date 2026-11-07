---
title: "Response results"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/response-results"
---

This article describes the API return result information for RDS for SQL Server.

<span id="http-status-code-description"></span>
## HTTP status code description


* The HTTP status code is 200, indicating that the interface request was successful.

* All HTTP status codes other than 200 indicate that the interface request failed. The specific failure information is returned in the form of JSON.


<span id="return-result-example"></span>
## **Return result example**

<span id="request-call-successfully-returns-result"></span>
### **Request call successfully returns result**

An example of the result returned after a successful request call is as follows:

```json
{ 
        "ResponseMetadata" : { 
          "RequestId": "52ece640-60ba-4cf9-bf34-302fb45eef4f", 
          "Action": "DescribeRegions", 
          "Version": "2022-01-01", 
          "Service": "rds_mssql", 
          "Region": "cn-beijing" 
          }, 
"Result ": { /* return information for specific business */ 
          "Regions":[ 
             { 
              "RegionId": "cn-beijing", 
"RegionName": "North China 2 (Beijing) " 
             } 
          ] 
    } 
}
```



* ResponseMetadata and its internal RequestId, Action, Version, Service, and Region are fixed fields that will be returned regardless of whether the request is successful or not, as long as an API request is initiated.

* RequestId is the unique identifier of an API request. If the API is abnormal, you can [submit a ticket ](https://console.byteplus.com/workorder/create)to contact technical support and provide this ID to help locate the problem.

* Result is a fixed field whose content is defined by different products. The field is not returned when the request call fails.

* Except for the fixed fields, the rest are fields defined by specific APIs. For fields returned by different APIs, please refer to the specific definitions in each API document.


<span id="request-call-failed-return-result"></span>
### **Request call failed Return result**

An example of the return result after the request call fails is as follows:

```json
{ 
   "ResponseMetadata" : { 
        "RequestId": "d78bbf4e-63a5-4937-ac3c-3767e7eddfbe", 
        "Action": "ListRegions", 
        "Version": "2022-01-01", 
        "Service": "rds_mssql", 
        "Region": "cn-beijing", 
        "Error": { 
            "Code": "Failed", 
            "Message": "The request processing has failed due to some unknown error, exception or failure." 
        } 
   } 
}
```



* When the request fails, the Error field must appear. The Error field contains the Code and Message fields, among which:

* Code represents the specific error code. You can first find the corresponding reason and solution in the public error code and the error code list corresponding to the current interface according to the error code.

* The message will give the specific reason why the error occurred, and this text may change as the business evolves or the experience is optimized.

* When the request call fails, the Result field is not returned.
