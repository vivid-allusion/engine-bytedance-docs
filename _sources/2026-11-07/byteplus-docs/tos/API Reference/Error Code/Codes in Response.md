---
title: "Codes in Response"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-codes-in-response"
---

This topic describes the status and error codes that can be encountered in server responses to requests.

<span id="eb29ea95"></span>
## **Status codes**

The response status codes are summarized below.


|**Status Code** |**Description** |
|---|---|
|2XX |The request succeeded, and the server has returned the data requested by the client. |
|4XX |The client's request contained errors, and the server did not create or modify data. |
|5XX |The server encountered an error, leaving the client unable to tell whether the sent request succeeded. |


<span id="7a7a050a"></span>
## **Error codes**

When there is an error in calling an API, no result data will be returned. You can identify related issues based on the error code and error message returned by the API. When an error occurs during API use, the server returns an HTTP status code of 3XX, 4XX, or 5XXand a response body containing the corresponding error code and message.

<span id="a386eab5"></span>
### **Error responses**

When an error occurs, the response includes the following:


* A corresponding HTTP status code of 3XX, 4XX, or 5XX.

* A response body carrying information about the error. The following sample error response shows the structure of response elements common to all REST error responses.


```JSON
{
    "Code" : "NoSuchKey",
    "Message" : "The resource you requested does not exist",
    "RequestId" : "4442587FB7D0A2F9",
    "HostId" : "",
    "Resource" : "/bucketName/objectName"
}
```


The REST error response elements are described below.


|**Name** |**Description** |
|---|---|
|Code |The error code is a stringthat uniquely identifies an error condition. |
|Message |A detailed description of the error. |
|RequestId |ID of the request returned for error locating. |
|HostId |ID of the server providing the response. |
|Resource |Bucket or object that is involved in the error. |


Many error responses include additional structured data to facilitate developers' understanding and diagnosis of programming errors. For example, if the Content\-MD5 header in your REST PUT request contains a digest that does not match the one calculated on the server, you will receive a BadDigest error. The error response also includes the server\-calculated digest and the expected digest. During development, you can use this information for error diagnosis.

<span id="baef8fb8"></span>
### **Error codes**

If an error occurs for a request to TOS, the response body contains an error code and a corresponding description.


|**Error Code** |**Description** |**HTTP Status Code** |**Handling** |
|---|---|---|---|
|PermanentRedirect |The bucket you are attempting to access must be addressed using the specified endpoint. Send all future requests to this endpoint. |301 Moved Permanently |Send requests to the new address returned. |
|WebsiteRedirect |The bucket name is missing in the Website request. |301 Moved Permanently |Retry after including the bucket name in the request. |
|TemporaryRedirect |You are being temporarily redirected to the bucket while the Domain Name System (DNS) server is being updated. |307 Moved Temporarily |You will be automatically redirected, or you can send the request to the redirected address. |
|CustomDomainAreadyExist |The configured domain already exists. |400 Bad Request |Configuration is already completed, and no further action is needed. |
|CustomDomainNotExist |You are deleting a nonexistent domain. |400 Bad Request |The domain is not configured or has already been deleted, and there is no need for deletion now. |
|MalformedError |The request contains improperly formatted XML. |400 Bad Request |Retry with proper XML formatting. |
|MetadataTooLarge |The metadata message headers exceed the maximum allowed size. |400 Bad Request |Reduce the size of the headers. |
|MissingSecurityHeader |The request lacks a required header. |400 Bad Request |Provide the required header. |
|EntityTooLarge |The uploaded object exceeds the maximum allowed size. |400 Bad Request |Modify the condition in the policy submitted in the POST request or reduce the object size. |
|EntityTooSmall |The uploaded object is smaller than the minimum allowed size. |400 Bad Request |Modify the condition in the policy submitted in the POST request or increase the object size. |
|BadDigest |The MD5 provided in the request does not match the MD5 calculated by the server. |400 Bad Request |Check if the MD5 in the header matches the MD5 calculated from the message body. |
|IncompleteBody |The request body is not fully received due to network or other issues. |400 Bad Request |Reupload the object. |
|InvalidArgument |Incorrect parameter format. |400 Bad Request |Adjust the parameters according to the error message in the response body. |
|InvalidBucket |The specified bucket is no longer available. |400 Bad Request |Change the bucket name. |
|BadDomainName |The domain name is invalid. |400 Bad Request |Check the domain name and use a valid one. |
|BadRequest |The request parameters are invalid. |400 Bad Request |Adjust according to the error message in the response body. |
|InvalidLocationConstraint |The specified Location for bucket creation is invalid or does not exist. |400 Bad Request |Specify a valid Location. |
|InvalidPart |One or more specified parts cannot be found. The parts may not have been uploaded, or the specified ETag does not match the ETag of the parts. |400 Bad Request |Provide a correct list of parts and ETags. |
|InvalidPartOrder |The part order is invalid. The part list must be arranged in ascending order by part number. |400 Bad Request |Retry merging after sorting in ascending order by part number. |
|IllegalLocationConstraintException |You are creating a bucket in a nondefault region without specifying Location. |400 Bad Request |Create the bucket in the default region or create it in a nondefault region with Location being specified. |
|InvalidRedirectLocation |The redirect address is invalid. |400 Bad Request |Specify a valid address as directed by the body message. |
|InvalidRequest |The request is invalid. |400 Bad Request |Adjust the request according to the error message in the response body. |
|InvalidRequestBody |The request body is invalid, or a request body is required but not provided. |400 Bad Request |Provide a properly formatted request body. |
|InvalidTargetBucketForLogging |An invalid bucket is specified for logging. |400 Bad Request |Retry after configuring the ACL setting of the target bucket. |
|KeyTooLongError |The key provided is too long. |400 Bad Request |Use a shorter key. |
|InvalidBucketName |The bucket name is invalid, either exceeding the length limit or containing prohibited characters. |400 Bad Request |Change the bucket name. |
|InvalidEncryptionAlgorithmError |The specified encryption algorithm is invalid. An encryption header is specified incorrectly for downloading an SSE\-C encrypted object, resulting in decryption failure. |400 Bad Request |Use the correct encryption header. |
|MalformedLoggingStatus |The XML format for logging is incorrect. |400 Bad Request |Retry with proper XML formatting. |
|MalformedPolicy |The bucket policy failed the verification. |400 Bad Request |Adjust the policy according to the error message in the response body and the requirements for bucket policies. |
|MalformedQuotaError |The XML format for Quota is incorrect. |400 Bad Request |Retry with proper XML formatting. |
|MalformedXML |You have sent an XML document with an incorrect format. |400 Bad Request |Retry with proper XML formatting. |
|MaxMessageLengthExceeded |You have sent a request with a message body when copying an object. |400 Bad Request |Retry copying without including a message body. |
|InvalidPolicyDocument |The content in the form does not match the conditions specified in the policy. |400 Bad Request |Adjust the form policy according to the error message in the response body and retry. |
|MissingRegion |The request lacks region information, and the system does not have a default region. |400 Bad Request |Include region information in the request. |
|MissingRequestBodyError |You have sent an empty XML document in the request. |400 Bad Request |Supply the correct XML document. |
|MissingRequiredHeader |The request lacks required headers. |400 Bad Request |Provide the required headers. |
|MalformedACLError |The format of the provided XML is invalid or noncompliant with TOS specifications. |400 Bad Request |Retry with proper XML formatting. |
|TooManyBuckets |You have attempted to create more buckets than are allowed for your account. |400 Bad Request |Retry after deleting some of your buckets. |
|TooManyWrongSignature |You have been denied service for too many erroneous requests. |400 Bad Request |Retry with the correct Access Key. |
|UnexpectedContent |The request requires a message body, but the client did not include it, or the request does not require a message body, but the client included it. |400 Bad Request |Retry as directed. |
|AccessDenied |Your access is denied because the request lacks a Date header or contains an improperly formatted header. |403 Forbidden |Include an appropriate Date header in the request. |
|InvalidAccessKeyId |The specified Access Key does not exist in the system. |403 Forbidden |Specify a valid Access Key. |
|RequestTimeTooSkewed |The difference between the request time and the server's time is too large. |403 Forbidden |Check if the client's time deviates too much from the current time. |
|AccessForbidden |You have no adequate permission. The bucket CORS rules may have denied your request, or the bucket has no CORS rules at all. |403 Forbidden |Modify the CORS configuration of the bucket or send an OPTIONS request matching the bucket's CORS configuration. |
|SignatureDoesNotMatch |The signature in the request does not match the signature calculated by the system. |403 Forbidden |Check your Secret Key and the signature calculation method. |
|NoSuchBucket |The specified bucket does not exist. |404 Not Found |Create the bucket before further operations. |
|NoSuchKey |The specified key does not exist. |404 Not Found |Upload the object first. |
|NoSuchBucketPolicy |The target bucket policy does not exist. |404 Not Found |Configure the bucket policy first. |
|NoSuchUpload |The specified multipart upload does not exist. The upload ID does not exist, or the multipart upload has been aborted or completed. |404 Not Found |Specify an existing multipart upload or reinitialize an upload. |
|NoSuchCORSConfiguration |The target CORS configuration does not exist. |404 Not Found |Create a CORS configuration first. |
|NoSuchLifecycleConfiguration |The target lifecycle configuration does not exist. |404 Not Found |Create the bucket lifecycle configuration first. |
|NoSuchVersion |The version ID specified in the request does not match any existing version. |404 Not Found |Use a valid version ID. |
|NoSuchWebsiteConfiguration |The requested Website does not exist. |404 Not Found |Configure the Website first. |
|MethodNotAllowed |The request method cannot be used on the requested resource. |405 Method Not Allowed |Use an allowed method. |
|RequestTimeout |No read/write operations were performed between you and the server within the socket connection timeout period. |408 Request Timeout |Retry after troubleshooting your network, or contact technical support. |
|BucketAlreadyExists |The specified bucket name already exists. The bucket namespace is shared by all TOS users. Retry with a different bucket name. |409 Conflict |Change the bucket name. |
|BucketNotEmpty |The bucket you are attempting to delete is not empty. |409 Conflict |Delete all objects from the bucket before deleting the bucket. |
|BucketAlreadyOwnedByYou |You have already created a bucket with this name and own it. |409 Conflict |The bucket already exists. There is no need for further bucket creation. |
|UpdateConflict |Concurrent updates to the same object key conflict. |409 Conflict |Avoid concurrent updates to the same key, or contact technical support. |
|MissingContentLength |The Content\-Length header is missing in the HTTP request. |411 Length Required |Provide the Content\-Length header. |
|PreconditionFailed |At least one of the preconditions that you specified did not hold. |412 Precondition Failed |Modify your request according to the Conditions in the response body. |
|InvalidRange |The range supplied in the request is invalid. |416 Client Requested Range Not Satisfiable |Retry with a valid range. |
|ExceedAccountQPSLimit |The account's QPS limit is exceeded. |429 StatusTooManyRequests |Reduce the QPS from the current account, or contact technical support. |
|ExceedAccountRateLimit |The account's bandwidth limit is exceeded. |429 StatusTooManyRequests |Reduce bandwidth usage from the current account, or contact technical support. |
|ExceedBucketQPSLimit |The bucket's QPS limit is exceeded. |429 StatusTooManyRequests |Reduce the QPS to the bucket, or contact technical support. |
|ExceedBucketRateLimit |The bucket's bandwidth limit is exceeded. |429 StatusTooManyRequests |Reduce bandwidth usage for accessing the bucket, or contact technical support. |
|InternalError |The system encountered an internal error. Please retry. |500 Internal Server Error |Contact technical support. |
|ServiceNotImplemented |The requested method is not implemented by the server. |501 Not Implemented |The functionality is currently not supported. Contact technical support. |
|ServiceUnavailable |Server overload or internal exception. |503 Service Unavailable |Retry later, or contact technical support. |
|SlowDown |Lower the frequency of requests. |503 Service Unavailable |Lower the frequency of requests. |
|PartSizeSmall |Parts smaller than a specified size cannot be merged (except for the last part). |400 Bad Request |Update the noncompliant parts. |
