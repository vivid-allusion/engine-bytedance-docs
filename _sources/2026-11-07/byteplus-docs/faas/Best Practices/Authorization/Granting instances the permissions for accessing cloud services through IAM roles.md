---
title: "Granting instances the permissions for accessing cloud services through IAM roles"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Granting_instances_the_permissions_for_accessing_cloud_services_through_IAM_roles"
---

BytePlus Function Service(FaaS) can access other BytePlus cloud services by using Identity and Access Management (IAM) roles. This prevents hardcoding the access key ID (AK) and secret access key (SK) of your account in code or environment variables, reducing the risk of access key leaks.

<span id="cLxPYsC2"></span>
## Background information

To enable a function to securely access other cloud resources, you can grant specific permissions to the function by using an IAM role, and use Security Token Service (STS) to generate temporary access credentials and manage the validity period of the permissions.

<span id="iW3r4wl2"></span>
## Considerations

STS temporary access credentials contain sensitive service information and need to be kept with caution.

<span id="DAgat2CG"></span>
## Limits

The maximum validity period of STS temporary access credentials is 12 hours. We recommend that you periodically obtain the latest access credentials to ensure they always remain valid.

<span id="na2NYimt"></span>
## Prerequisites


* The IAM policy required to access the target cloud service has been created. The predefined policy  on the platform  includes permissions for some commonly used cloud services. You can change the policy if it does not meet your business requirements. For the method of changing policies, see .

* A role that allows **veFaaS** to access the target cloud services has been created. For information on how to create a role, see .

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5cbfd86e2ed139c892a69de743fbf5b0.png) </span>


<span id="xV4pDyAO"></span>
## Procedure

<span id="jPg55N8A"></span>
### Step 1: Bind the target function to the created role

Bind the target function to the created role by using [CreateFunction](https://docs.byteplus.com/en/docs/faas/CreateFunction) or [UpdateFunction](https://docs.byteplus.com/en/docs/faas/UpdateFunction).


|Request parameters |Type |Example |Description |
|---|---|---|---|
|Role |String |trn:iam::140000\*\*\*\*:role/VeFaaSDefaultRole |Enter The Resource Name (TRN) code of the role to be bound to the function instance. You can view the **Role TRN** of the target role on the **Role detail** page of the [IAM console](https://console.byteplus.com/iam/identitymanage/role). |


<span id="Drz7qR8k"></span>
### Step 2: Obtain temporary credentials

After the function is bound to the IAM role and is deployed, you can obtain the STS token information, which includes the AK, SK, and session token, by using the request header or context.


* Web applications

   Inject the STS token into the request header. The following sample code shows how to extract the STS token in different programming languages.

   * Python

      ```Python
      from fastapi import FastAPI, Request
      app = FastAPI()
      
      @app.get('/')
      def index_handler(request: Request):
          request_id = request.headers.get("x-faas-request-id")
          
          access_key_id = request.headers.get("x-faas-access-key-id")    
          secret_access_key = request.headers.get("x-faas-secret-access-key")    
          session_token = request.headers.get("x-faas-session-token")
      ```
      

   * Node

      ```JavaScript
      import express from "express";
      
      const app = express();
      
      app.get("/", (req, res) => {
        const requestId = req.header("x-faas-request-id");
      
        const accessKeyId = req.header("x-faas-access-key-id");  
        const secretAccessKey = req.header("x-faas-secret-access-key");
        const sessionToken = req.header("x-faas-session-token");
      ```
      

   * Go

      ```Go
      func bizHandler(w http.ResponseWriter, r *http.Request) {
          requestId := r.Header.Get("X-Faas-Request-Id")
          
          ak := r.Header.Get("X-Faas-Access-Key-Id")    
          sk := r.Header.Get("X-Faas-Secret-Access-Key")    
          sessionToken := r.Header.Get("X-Faas-Session-Token")
          
      }
      ```
      

* Event function

   Inject the STS token into the request context. The following sample code shows how to extract the STS token in different programming languages.

   * Python

      ```Python
      def handler(event, context):
          request_id = getattr(context, "request_id", None)
              
          # Extract temporary credentials from the context object
          access_key_id = getattr(context, "access_key_id", None)
          secret_access_key = getattr(context, "secret_access_key", None)
          session_token = getattr(context, "session_token", None)
      ```
      

   * Node

      ```JavaScript
      exports.handler = async function handler(event, context) {
        // Extract temporary credentials from the context object  
        const { requestId, accessKeyId, secretAccessKey, sessionToken } = context;
      ```
      

   * Golang

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Before getting started, upgrade Golang to <code>v0.0.0-20250827</code> or later by executing <code>go get github.com/volcengine/vefaas-golang-runtime</code>.      </div>
      

      ```Go
      package main
      
      import (
              "context"
      
              "github.com/volcengine/vefaas-golang-runtime/events"
              "github.com/volcengine/vefaas-golang-runtime/vefaascontext"
      )
      
      func handler(ctx context.Context, payload interface{}) (*events.EventResponse, error) {   
          // Extract the STS token    
          ak := vefaascontext.AccessKeyIdFromContext(ctx)
          sk := vefaascontext.SecretAccessKeyFromContext(ctx)
          sessionToken := vefaascontext.SessionTokenFromContext(ctx)
      }
      ```
      

&nbsp;


<span id="WXOvvvhW"></span>
### Step 3: Call a cloud service

Call the cloud services you need through [SDK](https://docs.byteplus.com/en/docs/6662/1386370) by using a programming language accordingly. The following sample code shows how to use the Go SDK.


* Web Function


```Go
package main

import (
    "fmt"
    "log"
    "net/http"

    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func bizHandler(w http.ResponseWriter, r *http.Request) {
    ctx := r.Context()

    ak := r.Header.Get("X-Faas-Access-Key-Id")
    sk := r.Header.Get("X-Faas-Secret-Access-Key")
    sessionToken := r.Header.Get("X-Faas-Session-Token")

    cred := tos.NewStaticCredentials(ak, sk)
    cred.WithSecurityToken(sessionToken)

    // Use the corresponding TOS access domain name
    client, err := tos.NewClientV2("tos-ap-southeast-1.ivolces.com", tos.WithRegion("ap-southeast-1"),
        tos.WithCredentials(cred))
    if err != nil {
        errMsg := fmt.Sprintf("failed to create client: %v", err)
        log.Print(errMsg)
        http.Error(w, errMsg, http.StatusInternalServerError)
        return
    }

    getObjectOut, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{
        Bucket: "your-bucket",
        Key:    "your-key",
    })
    if err != nil {
        errMsg := fmt.Sprintf("failed to get object: %v", err)
        log.Print(errMsg)
        http.Error(w, errMsg, http.StatusInternalServerError)
        return
    }
    log.Printf("get object successfully, output: %+v", getObjectOut)

}
```



* Event function


```Go
package main

import (
    "context"
    "log"

    "github.com/volcengine/vefaas-golang-runtime/events"
    "github.com/volcengine/vefaas-golang-runtime/vefaascontext"
    volcVefaas "github.com/volcengine/volcengine-go-sdk/service/vefaas"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

func handler(ctx context.Context, payload interface{}) (*events.EventResponse, error) {
    // Extract STS Token
    ak := vefaascontext.AccessKeyIdFromContext(ctx)
    sk := vefaascontext.SecretAccessKeyFromContext(ctx)
    sessionToken := vefaascontext.SessionTokenFromContext(ctx)

    // Create Session Client
    config := volcengine.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, sessionToken)).WithRegion("ap-southeast-1")

    s, err := session.NewSession(config)
    if err != nil {
        log.Printf("failed to create session, error: %v", err)
        return nil, err
    }

    vefaasClient := volcVefaas.New(s)

    // Call the clould service API
    out, err := vefaasClient.GetFunction(&volcVefaas.GetFunctionInput{
        Id: volcengine.String("your-function-id"),
    })
    if err != nil {
        log.Printf("failed to get function, error: %v", err)
        return nil, err
    }
}
```


<span id="I82j9wox"></span>
### Step 4: Release a function

After you bind or update the IAM role, you need to release the function again to make the cloud service authorization take effect. For the method of releasing a function again, see [Releasing functions](https://docs.byteplus.com/en/docs/faas/Release_function).
