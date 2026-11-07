---
title: "Upload Callback (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-callback-go-sdk"
---

An upload callback refers to a process in which the client includes a callback parameter in its request. After the upload is completed, the server sends a synchronous POST callback request to the third\-party application server specified in the callback parameter. Only after the third\-party server confirms receipt and returns a result does the server return all results to the client.

For a detailed introduction to upload callbacks, see [Upload Callback](https://docs.byteplus.com/docs/tos/Upload-callback).

<span id="9b4cf5b9"></span>
## Sample Code

<span id="d5de9160"></span>
### Standard Upload: Upload Callback Implementation

```Go
package main

import (
    "context"
    "encoding/base64"
    "fmt"
    "os"
    "strings"

    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func checkErr(err error) {
    if err != nil {
       if serverErr, ok := err.(*tos.TosServerError); ok {
          fmt.Println("Error:", serverErr.Error())
          fmt.Println("Request ID:", serverErr.RequestID)
          fmt.Println("Response Status Code:", serverErr.StatusCode)
          fmt.Println("Response Header:", serverErr.Header)
          fmt.Println("Response Err Code:", serverErr.Code)
          fmt.Println("Response Err Msg:", serverErr.Message)
       } else if clientErr, ok := err.(*tos.TosClientError); ok {
          fmt.Println("Error:", clientErr.Error())
          fmt.Println("Client Cause Err:", clientErr.Cause.Error())
       } else {
          fmt.Println("Error:", err)
       }
       panic(err)
    }
}

func main() {
    var (
       
       ak = os.Getenv("TOS_ACCESS_KEY")
       sk = os.Getenv("TOS_SECRET_KEY")
       
       endpoint = "your endpoint"
       region   = "your region"
       
       bucketName = "*** Provide your bucket name ***"
      
       objectKey   = "*** Provide your object key ***"
       callbackUrl = "*** Provide your callback url ***"
    )
 
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(ak, sk)))
    checkErr(err)

   
 
    callback := `
    {
       "callbackUrl" : "` + callbackUrl + `", 
       "callbackBody" : "{\"bucket\": ${bucket}, \"object\": ${object}, \"key1\": ${x:key1}}", 
       "callbackBodyType" : "application/json"                
    }`
  
    callbackVar := `
    {
       "x:key1" : "ceshi"
    }`

    body := strings.NewReader("object content")
    output, err := client.PutObjectV2(context.Background(), &tos.PutObjectV2Input{
       PutObjectBasicInput: tos.PutObjectBasicInput{
          Bucket:      bucketName,
          Key:         objectKey,
          Callback:    base64.StdEncoding.EncodeToString([]byte(callback)),
          CallbackVar: base64.StdEncoding.EncodeToString([]byte(callbackVar)),
       },
       Content: body,
    })
    checkErr(err)
    fmt.Println("Put Object Request ID: ", output.RequestID)
    fmt.Println("Put Object Response Status Code: ", output.StatusCode)
}
```


<span id="04b3c44f"></span>
### Implementing upload callbacks for chunked uploads

```Go
package main

import (
    "context"
    "encoding/base64"
    "fmt"
    "os"

    "github.com/volcengine/ve-tos-golang-sdk/v2/tos"
)

func checkErr(err error) {
    if err != nil {
       if serverErr, ok := err.(*tos.TosServerError); ok {
          fmt.Println("Error:", serverErr.Error())
          fmt.Println("Request ID:", serverErr.RequestID)
          fmt.Println("Response Status Code:", serverErr.StatusCode)
          fmt.Println("Response Header:", serverErr.Header)
          fmt.Println("Response Err Code:", serverErr.Code)
          fmt.Println("Response Err Msg:", serverErr.Message)
       } else if clientErr, ok := err.(*tos.TosClientError); ok {
          fmt.Println("Error:", clientErr.Error())
          fmt.Println("Client Cause Err:", clientErr.Cause.Error())
       } else {
          fmt.Println("Error:", err)
       }
       panic(err)
    }
}

func main() {
    var (
       accessKey = os.Getenv("TOS_ACCESS_KEY")
       secretKey = os.Getenv("TOS_SECRET_KEY")
       
       endpoint = "your endpoint"
       region   = "your region"
      
       bucketName = "*** Provide your bucket name ***"

       
       objectKey = "*** Provide your object name ***"
       ctx       = context.Background()
       uploadId  = "*** Provide your upload id ***"
    
       parts = make([]tos.UploadedPartV2, 0)
       callbackUrl = "*** Provide your callback url ***"
    )

    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

   
    callback := `
    {
       "callbackUrl" : "` + callbackUrl + `", 
       "callbackBody" : "{\"bucket\": ${bucket}, \"object\": ${object}, \"key1\": ${x:key1}}", 
       "callbackBodyType" : "application/json"                
    }`
  
    callbackVar := `
    {
       "x:key1" : "ceshi"
    }`

    completeOutput, err := client.CompleteMultipartUploadV2(ctx, &tos.CompleteMultipartUploadV2Input{
       Bucket:      bucketName,
       Key:         objectKey,
       UploadID:    uploadId,
       Parts:       parts,
       Callback:    base64.StdEncoding.EncodeToString([]byte(callback)),
       CallbackVar: base64.StdEncoding.EncodeToString([]byte(callbackVar)),
    })
    checkErr(err)
    fmt.Println("CompleteMultipartUploadV2 Request ID:", completeOutput.RequestID)

}
```


<span id="60c3590e"></span>
### Sample Code for Verifying Callback Signatures

```Go
package main

import (
    "bytes"
    "crypto"
    "crypto/md5"
    "crypto/rsa"
    "crypto/x509"
    "encoding/base64"
    "encoding/pem"
    "errors"
    "fmt"
    "io/ioutil"
    "net/http"
    "sort"
)

const Authorization = "Authorization"
const XTosPublicKeyUrl = "x-tos-pub-key-url"

func calcStringToSign(req *http.Request, body []byte) []byte {
    buf := bytes.NewBuffer(nil)
    buf.WriteString(req.URL.Path)

    query := req.URL.Query()
    if len(query) > 0 {
       buf.WriteByte('?')
       keys := make([]string, 0, len(query))
       for key := range query {
          keys = append(keys, key)
       }
       sort.Strings(keys)

       for _, key := range keys {
          values := query[key]
          for _, value := range values {
             buf.WriteString(key)
             buf.WriteByte('=')
             buf.WriteString(value)
             buf.WriteByte('&')
          }
       }

       buf.Truncate(buf.Len() - 1)
    }

    buf.WriteByte('\n')
    buf.Write(body)
    return buf.Bytes()
}

func getSignature(r *http.Request) ([]byte, error) {
    authorization := r.Header.Get(Authorization)
    if authorization == "" {
       return nil, nil
    }

    return base64.StdEncoding.DecodeString(authorization)
}

func getPublicKey(r *http.Request) ([]byte, error) {
    var bytePublicKey []byte

    publicKeyURLBase64 := r.Header.Get(XTosPublicKeyUrl)
    if publicKeyURLBase64 == "" {
       return bytePublicKey, errors.New("no x-tos-pub-key-url field in request header ")
    }
    publicKeyURL, _ := base64.StdEncoding.DecodeString(publicKeyURLBase64)

    resp, err := http.Get(string(publicKeyURL))
    if err != nil {
       return bytePublicKey, err
    }

    bytePublicKey, err = ioutil.ReadAll(resp.Body)
    defer resp.Body.Close()
    if err != nil {
       return bytePublicKey, err
    }

    if resp.StatusCode >= http.StatusBadRequest {
       return nil, errors.New("get public key failed")
    }

    return bytePublicKey, nil
}

func getContentAndSignMD5(r *http.Request) ([]byte, []byte, error) {
    bodyContent, err := ioutil.ReadAll(r.Body)
    _ = r.Body.Close()
    if err != nil {
       return nil, nil, err
    }

    stringToSign := calcStringToSign(r, bodyContent)

    authMd5 := md5.New()
    authMd5.Write(stringToSign)
    signMd5 := authMd5.Sum(nil)
    return signMd5, bodyContent, nil
}

func verifySignature(publicKey []byte, signMd5 []byte, sign []byte) error {
    pubBlock, _ := pem.Decode(publicKey)
    if pubBlock == nil {
       return errors.New("invalid public key pem")
    }
    pubInterface, err := x509.ParsePKIXPublicKey(pubBlock.Bytes)
    if err != nil || pubInterface == nil {
       return errors.New("invalid public key pem")
    }

    pub := pubInterface.(*rsa.PublicKey)

    err = rsa.VerifyPKCS1v15(pub, crypto.MD5, signMd5, sign)
    if err != nil {
       return err
    }
    return nil
}

func CallbackHandler(w http.ResponseWriter, r *http.Request) {
    
    sign, err := getSignature(r)
    if err != nil {
       fmt.Println("get callback signature err:", err.Error())
       w.WriteHeader(http.StatusBadRequest)
       return
    }

   
    publicKey, err := getPublicKey(r)
    if err != nil {
       w.WriteHeader(http.StatusBadRequest)
       return
    }

    
    signMd5, body, err := getContentAndSignMD5(r)
    if err != nil {
       w.WriteHeader(http.StatusBadRequest)
       return
    }

    
    if err = verifySignature(publicKey, signMd5, sign); err != nil {
       w.WriteHeader(http.StatusUnauthorized)
       return
    }

    
    fmt.Println(body)
   
    w.WriteHeader(http.StatusOK)
    w.Write([]byte(`{"msg":"ok"}`))
    return
}
```
