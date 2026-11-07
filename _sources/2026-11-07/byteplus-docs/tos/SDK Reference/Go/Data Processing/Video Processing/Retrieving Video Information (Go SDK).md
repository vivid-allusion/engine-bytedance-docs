---
title: "Retrieving Video Information (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-video-information-go-sdk"
---

The video information retrieval function enables the acquisition of metadata for a specified video resource. This article describes how to retrieve video information using the TOS Go SDK.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to retrieve video information.

```go
package main

import (
    "context"
    "encoding/json"
    "fmt"
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
       } else {
          fmt.Println("Error:", err)
       }
       panic(err)
    }
}

type VideoInfo struct {
    Streams []struct {
       Index              int    `json:"index"`
       CodecName          string `json:"codec_name"`
       CodecLongName      string `json:"codec_long_name"`
       Profile            string `json:"profile"`
       CodecType          string `json:"codec_type"`
       CodecTagString     string `json:"codec_tag_string"`
       CodecTag           string `json:"codec_tag"`
       Width              int    `json:"width,omitempty"`
       Height             int    `json:"height,omitempty"`
       CodedWidth         int    `json:"coded_width,omitempty"`
       CodedHeight        int    `json:"coded_height,omitempty"`
       SampleAspectRatio  string `json:"sample_aspect_ratio,omitempty"`
       DisplayAspectRatio string `json:"display_aspect_ratio,omitempty"`
       PixFmt             string `json:"pix_fmt,omitempty"`
       Level              int    `json:"level,omitempty"`
       ChromaLocation     string `json:"chroma_location,omitempty"`
       Refs               int    `json:"refs,omitempty"`
       IsAvc              string `json:"is_avc,omitempty"`
       NalLengthSize      string `json:"nal_length_size,omitempty"`
       RFrameRate         string `json:"r_frame_rate"`
       AvgFrameRate       string `json:"avg_frame_rate"`
       TimeBase           string `json:"time_base"`
       StartPts           int    `json:"start_pts"`
       StartTime          string `json:"start_time"`
       DurationTs         int    `json:"duration_ts"`
       Duration           string `json:"duration"`
       BitRate            string `json:"bit_rate"`
       BitsPerRawSample   string `json:"bits_per_raw_sample,omitempty"`
       NbFrames           string `json:"nb_frames"`
       ExtradataSize      int    `json:"extradata_size"`
       Disposition        struct {
          Default         int `json:"default"`
          Dub             int `json:"dub"`
          Original        int `json:"original"`
          Comment         int `json:"comment"`
          Lyrics          int `json:"lyrics"`
          Karaoke         int `json:"karaoke"`
          Forced          int `json:"forced"`
          HearingImpaired int `json:"hearing_impaired"`
          VisualImpaired  int `json:"visual_impaired"`
          CleanEffects    int `json:"clean_effects"`
          AttachedPic     int `json:"attached_pic"`
          TimedThumbnails int `json:"timed_thumbnails"`
          Captions        int `json:"captions"`
          Descriptions    int `json:"descriptions"`
          Metadata        int `json:"metadata"`
          Dependent       int `json:"dependent"`
          StillImage      int `json:"still_image"`
       } `json:"disposition"`
       Tags struct {
          Language    string `json:"language"`
          HandlerName string `json:"handler_name"`
          VendorId    string `json:"vendor_id"`
       } `json:"tags"`
       SampleFmt     string `json:"sample_fmt,omitempty"`
       SampleRate    string `json:"sample_rate,omitempty"`
       Channels      int    `json:"channels,omitempty"`
       ChannelLayout string `json:"channel_layout,omitempty"`
    } `json:"streams"`
    Format struct {
       NbStreams      int    `json:"nb_streams"`
       NbPrograms     int    `json:"nb_programs"`
       FormatName     string `json:"format_name"`
       FormatLongName string `json:"format_long_name"`
       StartTime      string `json:"start_time"`
       Duration       string `json:"duration"`
       Size           string `json:"size"`
       BitRate        string `json:"bit_rate"`
       ProbeScore     int    `json:"probe_score"`
       Tags           struct {
          MajorBrand       string `json:"major_brand"`
          MinorVersion     string `json:"minor_version"`
          CompatibleBrands string `json:"compatible_brands"`
          Encoder          string `json:"encoder"`
       } `json:"tags"`
    } `json:"format"`
}

func main() {
    var (
       accessKey = os.Getenv("TOS_ACCESS_KEY")
       secretKey = os.Getenv("TOS_SECRET_KEY")
       
       endpoint = "your endpoint"
       region   = "your region"
       
       bucketName = "*** Provide your bucket name ***"

      
       videoKey = "video.mp4"
       ctx      = context.Background()
    )
    
    client, err := tos.NewClientV2(endpoint, tos.WithRegion(region), tos.WithCredentials(tos.NewStaticCredentials(accessKey, secretKey)))
    checkErr(err)

    
    style := "video/info" 
    out, err := client.GetObjectV2(ctx, &tos.GetObjectV2Input{Bucket: bucketName, Key: videoKey, Process: style})
    checkErr(err)
    var info VideoInfo
    err = json.NewDecoder(out.Content).Decode(&info)
    checkErr(err)
    fmt.Println("info:", info)

}
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to obtaining video information, please refer to [View Video Information](https://docs.byteplus.com/docs/tos/docs-viewing-video-information).
