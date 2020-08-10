
     # EasyPlayer.js

## 简介

集播放http-flv/WS-FLV , hls, websocket 于一身的H5`视频直播/视频点播`播放器, 使用简单, 功能强大；

## 功能说明

- [x] 支持 MP4 播放

- [x] 支持 m3u8/HLS 播放;

- [x] 支持 HTTP-FLV/WS-FLV 播放;

- [x] 支持 H265 播放;

- [x] 支持直播和点播播放;

- [x] 支持全屏显示;

- [x] 支持重连播放；

## HTML 集成示例

- 使用方式

- [x] 普通集成

copy  EasyWasmPlayer.js 到项目中

copy libDecoder.wasm到项目或者www的根目录（一定要根目录）

在 html 中引用 EasyWasmPlayer.js

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="../dist/EasyWasmPlayer.js"></script>
</head>
<body>
    <div style="width:600px;height:400px;background-color:black;margin-left:200px">
        <div id="265Player">
        </div>
        <script>
            callbackfun = function (e) {
                console.log(e);
            }
            var 265Player = new WasmPlayer(null,'265Player'，callbackFun,{cbUserPtr:this, decodeType:"auto", openAudio:1, BigPlay:false, Height:true})
        </script>
    </div>
</body>

</html>
```

- [x] vue集成

```
  npm install @easydarwin/easyplayer --save
```

- Vue 集成调用

copy node_modules/@easydarwin/easyplayer/EasyWasmPlayer.js 到 静态文件 根目录

copy node_modules/@easydarwin/easyplayer/libDecoder.wasm 到 项目 “根目录”


**注意：** 若出现libDecoder.wasm的文件错误是此文件路径不对

在 html 中引用 EasyWasmPlayer.js

#### demo

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width,initial-scale=1.0" />
    <link rel="icon" href="<%= BASE_URL %>favicon.ico" />
    <title>EasyPlayer-demo</title>
    <script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js"></script>
    <script src="./EasyWasmPlayer.js"></script>
  </head>
  <body>
    <noscript>
      <strong
        >We're sorry but easynvr-token doesn't work properly without JavaScript
        enabled. Please enable it to continue.</strong
      >
    </noscript>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
```
- [x] npm集成

```html
......

 <div style="width:600px;height:400px;background-color:black;margin-left:200px">
    <div id="265Player">
   </div>
 </div>

...... ...... import EasyPlayer from '@easydarwin/easyplayer'; ......
components: { EasyPlayer }
mounted(){
   var 265Player = new WasmPlayer(null,'265Player'，this.callbackFun,{cbUserPtr:this, decodeType:"auto", openAudio:1, BigPlay:false, Height:true})
},
methods:{
    callbackfun = function (e) {
                console.log(e);
            }
}
```



## 实例化参数

var player = new wasmPlayer(url,ID，callbackFun,{cbUserPtr:this, decodeType"auto", openAudio"1" or "0", BigPlay"true" or "false", Height:" true" or "false});

| 参数               | 说明                                             | 类型                       | 默认值 |
| ------------------ | ------------------------------------------------ | -------------------------- | ------ |
| url                | 视频地址                                          | String                     | null    |
| ID                 | 播放器实例的divID  (必传)                          | String                     | -      |
| callbackFun        | 事件回调                                          |                            | -      |
| cbUserPtr          | 自定义指针  (this的指向)                           |                            | this   |
| decodeType         | 解码类型                                           |                            | auto   |
| openAudio          | 是否打开音频                                       |Boolean                    | false   |
| BigPlay            | 是否开启大的播放按钮                                |Boolean                     | false  |
| Height             | 播放器尺寸是否继承父盒子的                          | Boolean                     | false |


### 录像播放相关属性
#### 注意：currentTime属性只在播放录像m3u8 有结束标记（#EXT-X-ENDLIST）的的流时生效。
play(url,autoplay,currentTime)
| 属性        | 说明                                   | 类型    | 默认值             |
| --------   | -------------------------------------- | ------- | ------------------|
| url        | 播放流地址                              | String | -                  |
| autoplay   |   是否自动播放                           | Boolean | 默认0             |
| currentTime|  视频开始时间(换算成秒)                   | Number | 默认this            |

## 事件

| 方法名     | 说明         | 参数                                                    |
| ---------- | ------------ | ---------------------                                  |
| play       | 播放事件      | url:'流地址',autoplay: '自动播放',currentTime:'开始时间' |
| pause      | 播放暂停     | -                                                       |
| stop       | 停止播放     | -                                                       |
| openAudio  | 打开声音      | -                                                      |
| closeAudio | 关闭声音      | -                                                      |
| startLoding| 开始加载动画  | -                                                   |
| endLoding  | 结束加载动画  | -                                                   |



## 更多流媒体音视频资源

EasyDarwin开源流媒体服务器：<a href="http://www.easydarwin.org" target="_blank" title="EasyDarwin开源流媒体服务器">www.EasyDarwin.org</a>

EasyDSS高性能互联网直播服务：<a href="http://www.easydss.com" target="_blank" title="EasyDSS高性能互联网直播服务">www.EasyDSS.com</a>

EasyNVR安防视频可视化服务：<a href="http://www.easynvr.com" target="_blank" title="EasyNVR安防视频可视化服务">www.EasyNVR.com</a>

EasyNVS视频综合管理平台：<a href="http://www.easynvs.com" target="_blank" title="EasyNVS视频综合管理平台">www.EasyNVS.com</a>

EasyNTS云组网：<a href="http://www.easynts.com" target="_blank" title="EasyNTS云组网">www.EasyNTS.com</a>

EasyGBS国标GB/T28181服务器：<a href="http://www.easygbs.com" target="_blank" title="EasyGBS国标GB/T28181视频服务器">www.EasyGBS.com</a>

EasyRTS应急指挥平台：<a href="http://www.easyrts.com" target="_blank" title="EasyRTS应急指挥平台">www.EasyRTS.com</a>

TSINGSEE青犀开放平台：<a href="http://open.tsingsee.com" target="_blank" title="TSINGSEE青犀开放平台">open.TSINGSEE.com</a>

Copyright © <a href="http://www.tsingsee.com" target="_blank" title="青犀TSINGSEE">www.TSINGSEE.com</a> Team 2012-2019

![青犀TSINGSEE](http://www.easydarwin.org/public/images/tsingsee_qrcode_160.jpg)

