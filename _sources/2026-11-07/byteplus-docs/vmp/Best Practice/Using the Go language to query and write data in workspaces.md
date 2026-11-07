---
title: "Using the Go language to query and write data in workspaces"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Writing_and_querying_workspace_data_using_Golang"
---

Vital Managed Service for Prometheus (VMP) workspaces are compatible with native Prometheus and support data writing and querying in Go. This topic describes the methods and examples of using the Go language to query and write data in workspaces.

<span id=".5YaZ5YWl5oyH5qCH5pWw5o2u"></span>
## Write metric data

<span id=".5L2_55SoIEJhc2ljQXV0aCDlhpnlhaXmjIfmoIc="></span>
### Write metrics through basic authentication

```go
package  main

import  (
   "context"
   "encoding/base64"
   "fmt"
   "net/http"
   "time"
   "github.com/castai/promwrite"
)

// NewRoundTripper ...
func NewRoundTripper(username, password  string)  http.RoundTripper {
   return  &basicAuthTransport{
            transport: http.DefaultTransport,
            basicAuth:  "Basic "  + base64.StdEncoding.EncodeToString([]byte(username+":"+password)),
      }

}

type  basicAuthTransport  struct  {
      transport http.RoundTripper
      basicAuth  string
}

func (bat *basicAuthTransport)  RoundTrip(req *http.Request) (*http.Response,  error) {
      req.Header.Add("Authorization", bat.basicAuth)
   return  bat.transport.RoundTrip(req)

}

func main()  {
   username := "username" // The username used for the basic authentication of the VMP workspace.
   password := "password" // The password used for the basic authentication of the VMP workspace.
   remotewriteURL := "remotewrite 地址" // You can copy the URL on the details page of the VMP workspace.
      c := promwrite.NewClient(remotewriteURL, promwrite.HttpClient(&http.Client{
            Transport: NewRoundTripper(username, password),
      }))
      resp, err := c.Write(context.Background(), &promwrite.WriteRequest{
            TimeSeries: []promwrite.TimeSeries{
                  {
                        Labels: []promwrite.Label{
                              {
                                    Name:    "__name__",
                                    Value:  "my_metric_name",
                              },
                        },
                        Sample: promwrite.Sample{
                              Time:  time.Now(),
                              Value:  123,
                        },
                  },
            },
      })
      fmt.Println(resp, err)

}
```


<span id=".5L2_55SoIEFLL1NLIOWGmeWFpeaMh-aghw=="></span>
### Write metrics through AK/SK authentication

```go
package main

import (
    "context"
    "fmt"
    "net/http"
    "time"
    
    "github.com/castai/promwrite"
    
    "github.com/volcengine/volc-sdk-golang/base"
)

// Config is the configuration for signing remote write requests with
// volcengine verification process. Empty values will be retrieved using the
// volcengine default credentials chain.
type Config struct {
   Region    string
   AccessKey string
   SecretKey string
   Service   string
}

// NewRoundTripper returns a new http.RoundTripper that will sign requests
// using Volcengine's Signature Verification signing procedure.
// Credentials for signing are retrieved using the the default volcengine credential
// chain. If credentials cannot be found, an error will be returned.
func NewRoundTripper(cfg *Config) (http.RoundTripper, error) {
   rt := &volcRoundTripper{
      next: http.DefaultTransport,
      signer: &base.Credentials{
         AccessKeyID:     cfg.AccessKey,
         SecretAccessKey: cfg.SecretKey,
         Region:          cfg.Region,
         Service:         cfg.Service,
      },
   }

   return rt, nil
}

type volcRoundTripper struct {
   next      http.RoundTripper
   signer    *base.Credentials
}

func (rt *volcRoundTripper) RoundTrip(req *http.Request) (*http.Response, error) {
   q := req.URL.Query()
   req.URL.RawQuery = q.Encode()
   return rt.next.RoundTrip(rt.signer.Sign(req))
}

func main() {
   rt, err := NewRoundTripper(&Config{
      Region:    "region", // The region of the workspace.
      AccessKey: "ak", // The access key ID of the user who is granted the remote write permission on VMP.
      SecretKey: "sk", // The secret access key of the user who is granted the remote write permission on VMP.
      Service:   "vmp",
   })
   if err != nil {
      panic(err)
   }

   remotewriteURL := "remotewrite 地址" // You can copy the URL on the details page of the VMP workspace.
   c := promwrite.NewClient(remotewriteURL, promwrite.HttpClient(&http.Client{
      Transport: rt,
   }))
   resp, err := c.Write(context.Background(), &promwrite.WriteRequest{
      TimeSeries: []promwrite.TimeSeries{
         {
            Labels: []promwrite.Label{
               {
                  Name:  "__name__",
                  Value: "my_metric_name",
               },
            },
            Sample: promwrite.Sample{
               Time:  time.Now(),
               Value: 123,
            },
         },
      },
   })
   fmt.Println(resp, err)
 }
```


<span id=".5p-l6K-i5oyH5qCH5pWw5o2u"></span>
## Query metric data

<span id=".5pSv5oyB5p-l6K-i55qE5o6l5Y-j"></span>
### Supported query endpoints


* [/api/v1/query](https://prometheus.io/docs/prometheus/latest/querying/api/#instant-queries)

* [/api/v1/query_range](https://prometheus.io/docs/prometheus/latest/querying/api/#range-queries)

* [/api/v1/series](https://prometheus.io/docs/prometheus/latest/querying/api/#finding-series-by-label-matchers)

* [/api/v1/labels](https://prometheus.io/docs/prometheus/latest/querying/api/#getting-label-names)

* [/api/v1/label/…/values](https://prometheus.io/docs/prometheus/latest/querying/api/#querying-label-values)


<span id=".5L2_55SoIEJhc2ljQXV0aCDmn6Xor6LmjIfmoIc="></span>
### Query metrics through basic authentication

The VMP APIs are compatible with native Prometheus. Therefore, you can use the existing Prometheus SDK when you call the APIs. The following section provides an example of how to use client_go.

```go
import  (
   "net/http"
   "strconv"
   "github.com/prometheus/client_golang/api"
      promv1  "github.com/prometheus/client_golang/api/prometheus/v1"
)

// NewPromAPI ...
func NewPromAPI(queryAddress, username, password  string)  (promv1.API,  error) {
      promClient, err := api.NewClient(api.Config{
            Address:      queryAddress,
            RoundTripper: NewBasicAuthRoundTripper(http.DefaultTransport, username, password),
      })
   if  err !=  nil  {
      return nil, err
      }
   return  promv1.NewAPI(promClient),  nil
}

// NewBasicAuthRoundTripper ...
func NewBasicAuthRoundTripper(next http.RoundTripper, username, password  string)  http.RoundTripper {
   if  next ==  nil  {
            next = http.DefaultTransport
      }
   return  &basicAuthTransport{
            transport: http.DefaultTransport,
            basicAuth:  "Basic "  + base64.StdEncoding.EncodeToString([]byte(username+":"+password)),
      }

}

type  basicAuthTransport  struct  {
      transport http.RoundTripper
      basicAuth  string
}

func (bat *basicAuthTransport)  RoundTrip(req *http.Request) (*http.Response,  error) {
      req.Header.Add("Authorization", bat.basicAuth)
   return  bat.transport.RoundTrip(req)

}

func main(){
    address := "vmp query 地址" // You can copy the URL on the details page of the VMP workspace.
    username := "username" // The username used for the basic authentication of the VMP workspace.
    password := "password" // The password used for the basic authentication of the VMP workspace.
    
    api, err := NewPromAPI(address, username, password)
    
    res, _, err := api.Query(context.TODO(), "up", time.Now())
    fmt.Println(res, err)
}
```


<span id=".5L2_55SoIEFLL1NLIOafpeivouaMh-aghw=="></span>
### Query metrics through AK/SK authentication

```go
import  (
   "context"
   "fmt"
   "net/http"
   "time"
   "github.com/prometheus/client_golang/api"
      promv1  "github.com/prometheus/client_golang/api/prometheus/v1"
   "github.com/volcengine/volc-sdk-golang/base"
)

// Config is the configuration for signing query requests with
// volcengine verification process. Empty values will be retrieved using the
// volcengine default credentials chain.
type  Config  struct  {
      Region        string // The access region.
      AccessKey  string // The service access key ID.
      SecretKey  string // The service secret access key.
      Service      string // The VMP service name, which is vmp.
}

type  volcRoundTripper  struct  {
      next   http.RoundTripper
      signer *base.Credentials

}

// NewRoundTripper returns a new http.RoundTripper that will sign requests
// using Volcengine's Signature Verification signing procedure.
//
// Credentials for signing are retrieved using the the default volcengine credential
// chain. If credentials cannot be found, an error will be returned.
func NewRoundTripper(cfg *Config)  (http.RoundTripper,  error) {
      rt := &volcRoundTripper{
            next: http.DefaultTransport,
            signer: &base.Credentials{
                  AccessKeyID:     cfg.AccessKey,
                  SecretAccessKey: cfg.SecretKey,
                  Region:          cfg.Region,
                  Service:         cfg.Service,
            },
      }

   return  rt,  nil
}

func (rt *volcRoundTripper)  RoundTrip(req *http.Request) (*http.Response,  error) {
      q := req.URL.Query()
      req.URL.RawQuery = q.Encode()
   return  rt.next.RoundTrip(rt.signer.Sign(req))

}

// NewPromClient ...
func NewPromClient(cfg *Config, queryAddress  string)  (promv1.API,  error) {
      rt, err := NewRoundTripper(cfg)
   if  err !=  nil  {
      return nil, err
      }
      promClient, err := api.NewClient(api.Config{
            Address:      queryAddress,
            RoundTripper: rt,
      })
   if  err !=  nil  {
      return nil, err
      }
   return  promv1.NewAPI(promClient),  nil
}

func main() {
   api, err := NewPromClient(&Config{
      Region:    "region",
      AccessKey: "ak",
      SecretKey: "sk",
      Service:   "vmp",
   }, "query地址") 
   if err != nil {
      fmt.Println(err.Error())
   }

   res, _, err := api.Query(context.TODO(), "up", time.Now())
   fmt.Println(res, err)
}
```


<span id=".57uT5p6c5aSE55CG"></span>
### Process results

Query results are generally of the ValVector or ValScalar type. You can process the results based on the following example. If the result type of QueryRange is prommodel.Matrix, you can extend the example as needed:

```go
func parseQueryResp(value prommodel.Value) (prommodel.Vector, error) {
   var samples prommodel.Vector
   var ok bool
   switch value.Type() {
   case prommodel.ValVector:
      samples, ok = value.(prommodel.Vector)
      if !ok {
         return nil, errors.New("convert result to \"model.Vector\"")
      }
   case prommodel.ValScalar:
      var scalar *prommodel.Scalar
      scalar, ok = value.(*prommodel.Scalar)
      if !ok {
         return nil, errors.New("convert result to \"model.Scalar\"")
      }
      samples = append(samples, &prommodel.Sample{
         Timestamp: scalar.Timestamp,
         Value:     scalar.Value,
      })
   default:
      return nil, errors.New("invalid query result")
   }
   return samples, nil
}
```
