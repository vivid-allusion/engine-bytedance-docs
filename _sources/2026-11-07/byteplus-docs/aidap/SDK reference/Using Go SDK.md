---
title: "Using Go SDK"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Using_Go_SDK"
---

This topic introduces the usage of the Go SDK for the AI Native BaaS for Supabase.

<span id="RD83Qseq"></span>
## Download and install

<span id="Z2P5Xy6y"></span>
### Prerequisites

Go 1.5 or above is required, and Go 1.12 or above is recommended.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can check the current Go version information by executing the <code>go version</code> command.</div>


<span id="2jojsFeT"></span>
### SDK download URL

For the AI Native Database Platform Go SDK source code address, refer to the [SDK list](https://docs.byteplus.com/en/docs/aidap/SDK_Overview).

<span id="UT7m1VCN"></span>
### **Install SDK**

Execute the following command under the target Go project to install the Go SDK.

```Plain Text
go get github.com/volcengine/volcengine-go-sdk/volcengine/credentials
go get github.com/volcengine/volcengine-go-sdk/volcengine/volcengineutil
```


<span id="Q9JPhngG"></span>
## Initialize client

The AI Native Database Platform Go SDK supports initializing clients through a session. Supabase clients created through a session implement reuse of HTTP/HTTPS resources (connections or requests) at the underlying level. When multiple clients need to be initialized for operations, creating them via Session can improve client performance.

<span id="ahRHd5Op"></span>
### Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* The Access Key ID (AK) and Secret Access Key (SK) information of the account have been obtained. For details, refer to [Managing Access Keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-keys).

* The supported region and corresponding host of the AI Native Database Platform have been obtained. Refer to [Service address](https://docs.byteplus.com/en/docs/aidap/Request_structure?lang=en).

* AI Native Database Platform Go SDK has been downloaded and installed.


<span id="4IZoK6fs"></span>
### Initialize client

Initialize the client with the following code.

```Go
package aidap

import (
    "fmt"
    "net/http"
    "sync"
    "time"

    "github.com/volcengine/volcengine-go-sdk/service/aidap"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
    "github.com/volcengine/volcengine-go-sdk/volcengine/credentials"
    "github.com/volcengine/volcengine-go-sdk/volcengine/session"
)

var (
    initOne     sync.Once
    initErr     error
    aidapClient *aidap.AIDAP
)

func init() {
    initOne.Do(func() {
       var (
          ak       string
          sk       string
          region   string
          endpoint string
          config   *volcengine.Config
          sess     *session.Session
       )
       ak = "Your AK"
       sk = "Your SK"
       region = "Your Region"  // For example, cn-beijing
       endpoint = "Your Endpoint" // AI Native BaaS for Supabase service address
       config = volcengine.NewConfig().WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
          WithRegion(region).WithEndpoint(endpoint)
       sess, initErr = session.NewSession(config)
       if initErr != nil {
          fmt.Printf("failed init aidap client, err=%s", initErr.Error())
          panic(initErr)
       }
       aidapClient = aidap.New(sess)
    })
}

func GetAidapClient() *aidap.AIDAP {
    return aidapClient
}
```


<span id="uR4DGLaj"></span>
## Sample

<span id="UMod1c3q"></span>
### Request timed out time settings

By default, no timeout is configured when you use the Go SDK to call APIs. You can specify the client's request timeout when initializing the client by using WithHTTPClient(&http.Client{Timeout: <timeout\> \* time.Second}). If the request is not completed within this time, it will be immediately terminated and report a timeout error. For example, you can set the client's request timeout to 10 seconds with the following code.

```Go
config = volcengine.NewConfig().
    WithCredentials(credentials.NewStaticCredentials(ak, sk, "")).
    WithRegion(region).
    WithHTTPClient(&http.Client{Timeout: 10 * time.Second})
```


<span id="er67hcZ3"></span>
### Sample

<span id="tmWYONNw"></span>
#### Creating a workspace

For the definitions, value ranges, and other information of the parameters used in the following SDK code, refer to [CreateWorkspace](https://docs.byteplus.com/en/docs/aidap/CreateWorkspace?lang=en).

```Go
package aidap

import (
    "encoding/json"
    "fmt"

    "github.com/volcengine/volcengine-go-sdk/service/aidap"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
)

// CreateWorkspace example: create a new workspace.
func CreateWorkspace() (*string, error) {
    client := GetAidapClient()
    input := &aidap.CreateWorkspaceInput{
       WorkspaceName: volcengine.String("test-workspace"),
       EngineVersion: volcengine.String(aidap.EnumOfEngineVersionForCreateWorkspaceInputSupabase124),
    }
    output, err := client.CreateWorkspace(input)
    if err != nil {
       fmt.Printf("CreateWorkspace failed with err: %v", err)
       return nil, err
    }
    result, err := json.Marshal(output)
    if err != nil {
       fmt.Printf("Marshal failed with err: %v", err)
       return nil, err
    }
    fmt.Printf("CreateWorkspace success, detail=%s", result)
    return output.WorkspaceId, nil
}
```


The parameters in this example are described in the following table.


|**Name** |**tip** |**Value** |
|---|---|---|
|WorkspaceName |Workspace name. The workspace name must meet the following rules:<br><br><br>* Can only contain Chinese characters, letters (a\-z and A\-Z), digits, hyphens (\-), and underscores (_).<br><br>* Must start with a Chinese character or letter (a\-z and A\-Z).<br><br>* Must be 2 to 64 characters in length.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not specified, the automatically generated workspace ID is used as the workspace name.</div><br> |test\-worksapce |
|EngineVersion |Engine version. Values:<br><br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `veDB_MySQL_8_0`: veDB MySQL 8.0.<br><br>* `Supabase_1_24`: Supabase 1.24. |PostgreSQL_17<br><br> |


<span id="7udWjhNm"></span>
#### Query workspace details

For the definitions, value ranges, and other information of the parameters used in the following SDK code, refer to [DescribeWorkspaceDetail](https://docs.byteplus.com/en/docs/aidap/DescribeWorkspaceDetail?lang=en).

```Go
package aidap

import (
    "encoding/json"
    "fmt"

    "github.com/volcengine/volcengine-go-sdk/service/aidap"
    "github.com/volcengine/volcengine-go-sdk/volcengine"
)

// DescribeWorkspaceDetail example: get detailed information of the workspace.
func DescribeWorkspaceDetail() error {
    client := GetAidapClient()
    workspaceId := "test-workspace-id"
    input := &aidap.DescribeWorkspaceDetailInput{
       WorkspaceId: volcengine.String(workspaceId),
    }
    output, err := client.DescribeWorkspaceDetail(input)
    if err != nil {
       fmt.Printf("DescribeWorkspaceDetail failed with err: %v", err)
       return err
    }
    result, err := json.Marshal(output)
    if err != nil {
       fmt.Printf("Marshal failed with err: %v", err)
       return err
    }
    fmt.Printf("DescribeWorkspaceDetail success, detail=%s", result)
    return nil
}
```


The parameters in this example are described in the following table.


|**Name** |**tip** |**Value** |
|---|---|---|
|WorkspaceId |ID of the workspace. |test\-workspace\-id |
