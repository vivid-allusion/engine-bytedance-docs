---
title: "Quick Start Guide (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Quick-start-ios-sdk"
---

This document presents common operations of the iOS SDK, including initialization, bucket creation, and so on.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before using the iOS SDK, please ensure that you have [installed the SDK](https://docs.byteplus.com/docs/tos/Install-ios-sdk).

<span id=".5q2l6aqk5LiA77ya5Yid5aeL5YyWLXRvcy3lrqLmiLfnq68="></span>
## Step 1: Initialize the TOS client

TOSClient is the iOS client for the TOS service, providing a series of methods for managing Buckets and Objects. Before sending requests to TOS using the iOS SDK, you must initialize TOSClient and configure the required parameters: AccessKey, SecretKey, Endpoint, and Region. For information on the Regions and Endpoints supported by TOS, please refer to [Regions and Access Domain Names](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Mobile devices constitute an untrusted environment; storing AccessKey and SecretKey information directly on the device and performing signature calculations poses extremely high risks. It is strongly recommended to use the STS authentication mode. For specific steps, please refer to <a href="https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service">Using STS Temporary AK/SK+Token to Access BytePlus TOS</a>.</div>


The following example demonstrates how to initialize TOSClient using STS:

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:accessKey secretKey:secretKey securityToken:securityToken];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:TOS_ENDPOINT withRegion:TOS_REGION];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];
```


<span id=".5q2l6aqk5LqM77ya6YWN572u6K-35rGC5Y-C5pWw"></span>
## Step 2: Configure Request Parameters

Before initiating an access request to a Bucket or Object, you must create the corresponding request structure and send it to TOS using the TOSClient initialized in the preceding steps.

An example request for creating a bucket is as follows:

```objectivec
TOSCreateBucketInput *create = [TOSCreateBucketInput new];
create.tosBucket = TOS_BUCKET;
create.tosAcl = TOSACLPublicRead;
TOSTask *task = [client createBucket:create];
```


<span id=".5q2l6aqk5LiJ77ya5aSE55CG6K-35rGC57uT5p6c"></span>
## Step 3: Processing Request Results

All operations in the iOS SDK return a TOSTask. You can use the `task` to query the execution status of the request and obtain the returned result from it. You can also use `continueWithBlock` to set asynchronous callback logic.

```objectivec
[task continueWithBlock:^id _Nullable(TOSTask * _Nonnull t) {
    if (!t.error) {
        NSLog(@"Create bucket success.");
        TOSCreateBucketOutput *output = t.result;
        NSLog(@"Bucket location: %@", output.tosLocation);
    } else {
        NSLog(@"Create bucket failed, error: %@.", t.error);
    }
    return nil;
}];
```


You can also use `waitUntilFinished` to achieve synchronous waiting.

```objectivec
[task waitUntilFinished];
```
