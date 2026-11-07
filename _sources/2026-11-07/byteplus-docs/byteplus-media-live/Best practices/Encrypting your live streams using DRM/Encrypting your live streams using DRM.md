---
title: "Encrypting your live streams using DRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-encrypting-your-live-streams-using-drm"
---

To protect high\-value content such as paid events and exclusive live streams from unauthorized redistribution, the industry\-standard security solution is Digital Rights Management (DRM) encryption. This topic provides the complete procedure for enabling DRM protection in BytePlus MediaLive.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus MediaLive supports the following DRM systems: Widevine, FairPlay, and PlayReady.</div>


<span id="d1baef6b"></span>
## Limitations


* BytePlus MediaLive only provides DRM\-encrypted playback addresses in HLS with MPEG\-TS and LL\-DASH with CMAF.

* We recommend using standard DRM players to play DRM\-encrypted live streams on web browsers. The performance of native Android players or other platforms may not be guaranteed.


<span id="7aed754a"></span>
## Procedure

The procedure includes the following steps:


1. Acquire the DRM key from your DRM licensing provider.

2. Configure DRM in the BytePlus MediaLive console.

3. Generate a playback address that is encrypted with DRM.

4. Decrypt the content for authorized users.


<span id="941c05bb"></span>
### Acquiring the DRM key

You must first acquire a DRM key from [Intertrust](https://www.expressplay.com/). For detailed instructions on obtaining the key, please refer to [Acquiring a DRM key](https://docs.byteplus.com/docs/byteplus-media-live/docs-acquiring-a-drm-key).

To enable encryption on Apple devices, it is also necessary to obtain a FairPlay certificate. You will then need to upload the certificate to the BytePlus MediaLive console and Intertrust. For instructions on acquiring the certificate and other related information, please refer to [Acquiring a FairPlay certificate](https://docs.byteplus.com/docs/byteplus-media-live/docs-acquiring-a-fairplay-certificate).

<span id="3b790e5c"></span>
### Configuring DRM in the BytePlus MediaLive console


1. Upload the DRM key and FairPlay certificate to BytePlus MediaLive. Please refer to [Managing DRM licenses](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-drm-licenses) for detailed instructions on how to upload the key and certificate.

2. In the BytePlus MediaLive console, configure a transcoding task for the domain name and AppName you want to encrypt. For details, refer to [Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding). As an example, suppose you want to encrypt Ultra\-high\-definition (UHD) streams for AppName "drm\-test". Configure as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/107f86e4900b4fed9f8f81d50f162adb~tplv-goo7wpa0wc-image.image) </span>

   * **Domain name space**: example.push.com

   * **AppName**: drm\-test

   * **Suffix**: _uhd

3. Configure DRM encryption for the domain name and AppName you want to encrypt. You can refer to [Configuring a DRM encryption task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-drm-encryption-task) for detailed instructions. In this example, configure as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a1ad5b655e54e6580fe768977e6354d~tplv-goo7wpa0wc-image.image) </span>

   * **Domain name space**: example.push.com

   * **AppName**: drm\-test

   * **Transcoding**: _uhd


<span id="4763a627"></span>
### Generating an encrypted playback address

You can generate a DRM\-encrypted playback address with the Address Generator.


1. Go to [Address Generator](https://console.byteplus.com/live/main/locationGenerate) and enter the corresponding information:

   * **Select a domain name**: example.pull.com. This should be the domain name for stream pulling that is associated with example.push.com, which you entered in the previous step. You can refer to [Domain name space](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary#Vhost) for more information about the relationship between these concepts.

   * **AppName**: drm\-test

   * **StreamName**: Enter your stream name

   * **Transcoding template**: _uhd

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e4db9069fee45f18bf37818642db0b7~tplv-goo7wpa0wc-image.image) </span>

2. Click **Generate address**.

3. Locate the M3U8 address, which contains a DRM tag. Use this address as the playback address.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9d4b1f5a5f547d38e86d00745cbf60d~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Playback addresses in other formats are not encrypted. To prevent users from accessing the live stream via these addresses, you can enable URL authentication for your domain name, or restrict user access to certain protocols. For details, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication">URL authentication</a> and <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-protocol-restrictions">Protocol restrictions</a>.</div>


* <div data-tips="true" data-tips-type="tip">If you want a playback address in the CMAF format, please <a href="https://console.byteplus.com/workorder/create">contact technical support</a>.</div>



<span id="70daa99f"></span>
### Decrypting the content

To allow authorized users to view encrypted live streams, the player needs to call the BytePlus OpenAPI to retrieve the DRM license. For iOS users, the player also needs to retrieve the FairPlay certificate.


* To retrieve the DRM license, call the [DescribeLicenseDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describelicensedrm) endpoint.

* To retrieve the FairPlay certificate, call the [DescribeCertDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm) endpoint.


<span id="58cd651a"></span>
#### Sample code for generating the authorization validation URL on your server

Since your BytePlus AK/SK cannot be stored on your client devices, you need to first generate the OpenAPI authentication information on your server and then pass the information to your client devices. You can either follow the instructions in [Signing BytePlus MediaLive requests](https://docs.byteplus.com/docs/byteplus-media-live/docs-signing-byteplus-medialive-requests) or use the [Server SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk) to calculate the signature.

Suppose you use the [Go SDK](https://github.com/byteplus-sdk/byteplus-sdk-golang) to call the BytePlus MediaLive OpenAPI. Use the following code to generate the query URLs that the client uses to retrieve the DRM license and FairPlay certificate.


1. Define the parameter values.

   ```Go
   var (
     serviceInfo = &ServiceInfo{
      Timeout: 5 * time.Second,
      Host:    "open.byteplusapi.com",
      Header: http.Header{
       "Accept": []string{"application/json"},
      },
      Credentials: Credentials{Region: RegionApSingapore, Service: "live"},
     }
     
     // API endpoints that need to be signed
     apiList = map[string]*ApiInfo{
      "DescribeLicenseDRM": {
       Method: http.MethodPost,
       Path:   "/",
       Query: url.Values{
        "Action":     []string{"DescribeLicenseDRM"},
        "Version":    []string{"2023-01-01"},
        "Vhost":      []string{"drm.test.com"},
        "Domain":     []string{"drmpull.videoarch.com"},
        "App":        []string{"app-drm"},
        "StreamName": []string{"s-drm-1221"},
        "DRMType":    []string{"fp"}, // The DRM encryption type
       },
      },
      "DescribeCertDRM": {
       Method: http.MethodGet,
       Path:   "/",
       Query: url.Values{
        "Action":  []string{"DescribeCertDRM"},
        "Version": []string{"2023-01-01"},
        "Vhost":   []string{"drm.test.com"},
        "App":     []string{"app-drm"},
       },
      },
     }
   )
   ```
   

2. Generate the query URLs with which the client retrieves the DRM license and FairPlay certificate.

   ```Go
   func TestClient_GetSignUrl(t *testing.T) {
     client := NewClient(serviceInfo, apiList)
     client.SetAccessKey("your ak")
     client.SetSecretKey("your sk")
     urlStr, _ := client.GetSignUrl("DescribeLicenseDRM", nil)
     fmt.Println("https://live-gateway-byteplus.byteintlapi.com/drm_api/?" + urlStr)
     urlStr, _ = client.GetSignUrl("DescribeCertDRM", nil)
     fmt.Println("https://live-gateway-byteplus.byteintlapi.com/drm_api/?" + urlStr)
   }
   ```
   


<span id="29770d52"></span>
#### Sample code for playing DRM\-encrypted streams on the client

Create a player on the client and perform DRM authorization validation.


* Web: The following sample code shows how to use the Player SDK for Web to play a DRM\-encrypted stream on iOS.

   ```objectivec
   VePlayer.createLivePlayer({ 
       url: 'https://xxx.m3u8', 
       height: 360, 
       drm: { 
         fairplay: { 
           getDrmConfig: async ({url}) => { 
             return { 
                // URL for getting the FairPlay certificate.
                serverCertificatePath: 'https://xxx', 
                // URL for getting the DRM license.
                serverProcessSPCPath: 'https://xxx', 
             } 
           }, 
         }, 
       }, 
     }).then(function (veplayer) { 
       veplayer.on('error', function (error) { 
         // Error code 7100 indicates that DRM authorization validation failed. Check whether the URLs for getting the DRM license and FairPlay certificate are valid. 
         console.log(error.errorCode); 
       }); 
     }); 
   ```
   

* iOS: The following sample code shows how to use the Player SDK for iOS to play a DRM\-encrypted stream on iOS.

   1. Initialize the player.

      ```objectivec
      self.livePlayer = [[TVLManager alloc] initWithType:VeLivePlayerTypeSystem];
      ```
      

   2. Configure the playback address for the DRM\-encrypted stream.

      ```objectivec
      NSString *playUrl = "http://pull.example.com/live/stream.m3u8";
      [self.livePlayer setPlayUrl:playUrl];
      ```
      

   3. After registering the observer, use the following callback methods to return the FairPlay certificate and the DRM license URL.

      ```objectivec
      - (NSData *)getDrmResourceLoaderCertificateData:(TVLManager *)player { 
          // Path to the FairPlay certificate.
          NSString *filePath = [[NSBundle mainBundle] pathForResource:@"testfairplay" ofType:@"cer"]; 
          NSData *certificate = [NSData dataWithContentsOfFile:filePath]; 
          return certificate; 
      } 
       
      - (NSString *)getDrmResourceLoaderLicenseUrl:(TVLManager *)player { 
          // Return the DRM license URL.
          return @"https://drmtest/license"; 
      }
      ```
      

   4. Call the [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play) method to play the DRM\-encrypted stream.

      ```objectivec
      [self.livePlayer play];
      ```
