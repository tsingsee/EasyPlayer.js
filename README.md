# 文档

## 简介

EasyPlayer.js H5播放器，是一款能够同时支持HTTP、HTTP-FLV、HLS（m3u8）、WS、WEBRTC、FMP4视频直播与视频点播等多种协议，支持H.264、H.265、AAC等多种音视频编码格式，支持MSE、WASM、WebCodec等多种解码方式，支持Windows、Linux、Android、iOS全平台终端的H5播放器，使用简单, 功能强大。

## 功能说明
- [x] 支持 MSE H264和H265硬解码;
- [x] 支持 WebCodec H264和H265硬解码;
- [x] 支持 WASM H264和H265硬解码/软解码;
- [x] 支持 m3u8/HLS (H265/H265)播放;
- [x] 支持 Mpeg4格式(H264)播放;
- [x] 支持 HTTP-FLV/WS-FLV (H265/H265)播放;
- [x] 支持 HTTP-FMP4/WS-FMP4 (H265/H265)播放;
- [x] <支持 WEBRTC(easy支持H264/H265、其他流媒体支持H264)播放;
- [x] 支持 裸流(H264/H265) 播放;
- [x] 支持 直播和点播播放;
- [x] 支持 点播多清晰度播放;
- [x] 支持 全屏或比例显示;
- [x] 支持 电子放大;
- [x] 支持 水印(动态水印、幽灵水印);
- [x] 支持 显示上一个视频最后一帧;
- [x] 支持 播放器快照截图;
- [x] 支持 视频录制(WebM格式(音频+视频)、Mp4格式(视频),Flv格式(音频+视频));
- [x] 支持 超时、断网重连、异常暂停播放等;

## 案例演示
[演示地址][1] 
[1]: https://www.tsingsee.com/easyplayer/

## 配置属性

| 参数               | 说明                                             | 类型                       | 默认值 |
| ------------------ | ------------------------------------------------ | -------------------------- | ------ |
| container                | 播放器容器       | -                     | - |
| decoder                | wasm解码地址       | String | - |
| isResize | 是否拉伸 | Boolean | true |
| loadingText                | 加载显示的文字       | String                     | 加载中 |
| videoBuffer                | 加载显设置最小缓冲时长，单位秒，播放器会自动消除延迟。示的文字       | Number                     | 1 |
| hasAudio | 是否解析音频 | Boolean | true |
| useMSE | MSE模式 | Boolean | fasle |
| useWCS | WCS模式 | Boolean | fasle |
| useSIMD        |强制使用wasm模式                                     | Boolean                    | false   |
| background             | 视频封面图片                                     | String                     | -      |
| qualityConfig         | 配置清晰      | Array | ['普清', '高清', '超清', '4K', '8K']   |
| defaultStreamQuality  |  默认显示的清晰度，如果不设置，会显示第一个清晰度                                    | String | -   |
| isNotMute | 是否渲染音频 | Boolean | false |
| recordType | 视频录制默认mp4格式 | String | mp4,flv |
| playbackForwardMaxRateDecodeIFrame | 录像倍数 | Number | - |
| debug | 控制台日志打印 | Boolean | false |
| debugLevel | 打印日志级别默认warn | String | debug,warn |



## 事件回调

| 事件名      | 说明         |
| ---------- | ------------ |
| play       | 播放事件      |
| pause      | 暂时事件      |
| videoInfo      | 视频信息      |
| audioInfo      | 音频信息      |
| mute      | 音频      |
| error      | 播放异常      |
| kBps      | 当前网速， 单位KB 每秒1次,      |
| recordEnd      | 录制结束的事件    |
| recordStart      | 录制开始的事件    |
| fullscreen | 当前是否全屏|
| streamQualityChange | 清晰度回调 |
| playbackSeek | 录像时间轴跳转回调 |
| playbackPreRateChange | 录像倍数的回调 |
| currentPts | 监听当前渲染帧的时间戳（流里面的）|

案例 
```js
EasyPlayrPro.on('play', function () {
    console.log('play');
})
```

错误 Type 类型说明
```js

playError = 'playError'/** 播放错误，url 为空的时候，调用 play 方法 */
fetchError = 'fetchError'/** http 请求失败 */
websocketError = 'websocketError'/** websocket 请求失败 */
wasmDecodeError = 'wasmDecodeError'/** wasm 解码失败 */
hlsError = 'hlsError'/** hls 解码失败 */
webrtcError = 'webrtcError'/** webrtc 解码失败 */
webrtcClosed = 'webrtcClosed',/** webrtc 关闭 */
flvDemuxBufferSizeTooLarge = 'flvDemuxBufferSizeTooLarge'/** 缓冲区过大*/
audioChannelError = 'audioChannelError'/** 音频错误*/

EasyPlayrPro.on('error', function (type, msg) {
    console.log('error:', type, msg);
})
// 说明: type为错误类型，msg为错误详情。
```
## 方法

| 方法名      | 说明         | 参数                  |
| ---------- | ------------ | ---------------------|
| play         | 播放      |         'url'            |
| playback       | 播放录像      |
| pause      | 暂停播放    |               |
| isPause      | 返回是否暂停中状态    |               |
| setBufferTime      |  设置最大缓冲时长    |           1    |
| setVolume      | 设置音量    |               |
| getVolume      | 获取音量    |               |
| exitFullscreen      | 退出全屏    |               |
| mute      | 静音    |               |
| cancelMute      | 取消静音    |               |
| isMute      |  返回是否静音    |               |
| screenshot         | 获取快照      |          |
| setFullscreen      |  全屏(取消全屏)播放视频    |               |
| setStreamQuality      |  设置分辨率必须是qualityConfig里面的数据    |               |
| forward      |  设置录像倍数    |               |
| setPlaybackStartTime      |  设置录像跳转时间/s     |               |
| getVideoInfo      |  获取视频信息    |               |
| getAudioInfo      |  获取音频信息    |               |
| destroy      | 关闭视频，释放底层资源    |               |

screenshot 截图，调用后弹出下载框保存截图

    filename: 可选参数, 保存的文件名, 默认 时间戳
    format : 可选参数, 截图的格式，可选png或jpeg或者webp ,默认 png
    quality: 可选参数, 当格式是jpeg或者webp时，压缩质量，取值0 ~ 1 ,默认 0.92
    type: 可选参数, 可选download或者base64或者blob，默认download
案例:
```js
const base64 = EasyPlayerPro.screenshot("test", "png", 0.5, 'base64')
```


## 更多流媒体音视频资源

EasyDarwin开源流媒体服务器：<a href="http://www.easydarwin.org" target="_blank" title="EasyDarwin开源流媒体服务器">www.EasyDarwin.org</a>

EasyDSS高性能互联网直播服务：<a href="http://www.easydss.com" target="_blank" title="EasyDSS高性能互联网直播服务">www.EasyDSS.com</a>

EasyNVR安防视频可视化服务：<a href="http://www.easynvr.com" target="_blank" title="EasyNVR安防视频可视化服务">www.EasyNVR.com</a>

EasyNVS视频综合管理平台：<a href="http://www.easynvs.com" target="_blank" title="EasyNVS视频综合管理平台">www.EasyNVS.com</a>

EasyNTS云组网：<a href="http://www.easynts.com" target="_blank" title="EasyNTS云组网">www.EasyNTS.com</a>

EasyGBS国标GB/T28181服务器：<a href="http://www.easygbs.com" target="_blank" title="EasyGBS国标GB/T28181视频服务器">www.EasyGBS.com</a>

EasyRTS应急指挥平台：<a href="http://www.easyrts.com" target="_blank" title="EasyRTS应急指挥平台">www.EasyRTS.com</a>

TSINGSEE青犀开放平台：<a href="http://open.tsingsee.com" target="_blank" title="TSINGSEE青犀开放平台">open.TSINGSEE.com</a>

Copyright © <a href="http://www.tsingsee.com" target="_blank" title="青犀TSINGSEE">www.TSINGSEE.com</a> Team 2012-2024

![青犀TSINGSEE](https://www.tsingsee.com/_nuxt/img/TSINGSEE.c72f9d0.jpg)
