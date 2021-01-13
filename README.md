# EasyPlayer.js

## 简介

EasyPlayer.js H5播放器，是一款能够同时支持HTTP、HTTP-FLV、HLS（m3u8）视频直播与视频点播等多种协议，支持H.264、H.265、AAC等多种音视频编码格式，支持mse、wasm等多种解码方式，支持Windows、Linux、Android、iOS全平台终端的H5播放器。


## 功能说明

- [x] 支持 m3u8/HLS 播放;

- [x] 支持 HTTP-FLV/WS-FLV 播放;

- [x] 支持 H265 播放;

- [x] 支持直播和点播播放;

- [x] 支持全屏显示;

- [x] 支持重连播放；

<br/>

## 集成使用示例

- **普通集成**

##### 1.引入
copy  EasyWasmPlayer.js 到项目中

copy libDecoder.wasm到项目或者www的根目录（一定要根目录）

##### 2.在 html 中引用 EasyWasmPlayer.js
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EasyWasmPlayer-Demo</title>
    <script src="./EasyWasmPlayer.js"></script>
    <style>
      .box {
        width:600px;
        height:400px;
      }
    </style>
</head>
<body>
    <div class="box">
      <div id="Player"></div>
    </div>
    <script>
      // 实例化播放器
      var Player = new WasmPlayer(null,'Player'，callbackFun,{cbUserPtr:this, decodeType:"auto", openAudio:1, BigPlay:false, Height:true});
      // 调用播放
      Player.play('url', 1)
    </script>
</body>

</html>
```
<br/>

- **VUE集成**

##### 1.下载
```
  npm install @easydarwin/easywasmplayer --save
```

##### 2.拷贝
Vue-Cli3.0 环境下

copy node_modules/@easydarwin/easywasmplayer/EasyWasmPlayer.js 到项目public目录下

copy node_modules/@easydarwin/easywasmplayer/libDecoder.wasm 到项目public目录下

##### 3.在项目public目录index.html引入
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width,initial-scale=1.0" />
    <link rel="icon" href="<%= BASE_URL %>favicon.ico" />
    <title>EasyWasmPlayer-Demo</title>
    <script src="./EasyWasmPlayer.js"></script>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

##### 4.VUE中使用
```vue
<template>
  <div class="box">
    <div id="Player"></div>
  </div>
</template>
<script>

export default {
  data() {
    return {
      player: '',
      url: 'http://127.0.0.1:10080/fvod/PnCsnxdMg/video.m3u8'
    }
  },
  mounted() {
    // 实例化播放器
    this.player = new WasmPlayer(null, 'Player', this.callbackfun)
    // 调用播放
    this.player.play(this.url, 1)
  },
  methods: {
    callbackfun(e) {
      console.log('callbackfun', e);
    }
  }  
}
</script>
<style>
  .box {
    width:600px;
    height:400px;
  }
</style>
```
## <a href="http://www.easydarwin.org/easywasmplayer/" target="_blank" title="在线演示">在线演示</a><br/>

**注意：** 若出现libDecoder.wasm的文件报404错误，提示找不到libDecoder.wasm文件，一定要排查是否存放在项目的根目录。

## 实例化参数

var player = new wasmPlayer(url,ID，callbackFun,{cbUserPtr:this,cfKbs: fn, decodeType:"auto" or "soft", openAudio"1" or "0", BigPlay"true" or "false", Height:" true" or "false, HideKbs:" true" or "false});

| 参数               | 说明                                                                                                              | 类型                       | 默认值 |
| ------------------ | ---------------------------------------------------------------------------------------------------------------- | -------------------------- | ------ |
| url                | 视频地址                                                                                                          | String                     | null    |
| ID                 | 播放器实例的divID(必传)                                                                                            | String                     | -      |
| decodeType         | 解码类型(auto：默认，soft：强制H265解码)                                                                            | String                      | auto   |
| openAudio          | 是否打开音频                                                                                                       | Boolean                    | false   |
| BigPlay            | 是否开启大的播放按钮                                                                                                | Boolean                     | false  |
| Height             | 播放器尺寸是否继承父盒子的                                                                                           | Boolean                     | false |
| HideKbs            | 是否隐藏实时码率                                                                                                    | Boolean                     | false |
| cfKbs              | 码率速率回调(averageKbps:平均传输速率，averageKbs: 平均码率，currentKbps: 当前传输速率，currentKbs: 当前码率)           | function                    | -      |
| callbackFun        | 事件回调                                                                                                            | function                    | -      |
| cbUserPtr          | 自定义指针(this的指向)                                                                                               |                            | this   |


### 录像播放相关属性
#### 注意：currentTime属性只在播放录像m3u8 有结束标记（#EXT-X-ENDLIST）的的流时生效。
play(url,autoplay,currentTime)
| 属性        | 说明                                        | 类型    | 默认值             |
| --------   | ---------------------------------------------     | ------- | ------------------|
| url        | 播放流地址                                   | String | -                  |
| autoplay   | 是否自动播放(0：默认，1：自动播放)             | Number | 0                  |
| currentTime| 视频开始时间(换算成秒)                        | Number | 0                  | 

## 事件

| 方法名      | 说明            | 参数                                                    |
| ----------  | ------------    | ---------------------                                  |
| play        | 播放事件        | url:'流地址',autoplay: '自动播放',currentTime:'开始时间' |
| pause       | 播放暂停        | -                                                       |
| destroy     | 停止播放        | -                                                       |
| openAudio   | 打开声音        | -                                                      |
| closeAudio  | 关闭声音        | -                                                      |
| startLoading | 开始加载动画    | -                                                       |
| endLoading   | 结束加载动画    | -                                                       |
| fullScreen  | 开启或退出全屏  | -                                                     |
| setSnap     | 设置封面照      | 封面图片地址                                          |
| endSnap     | 清除封面照      | -                                                     |


<br/>

### ✈ 更多视频解决方案资源汇总

- 流媒体技术：<br/>
© EasyDarwin开源流媒体服务器：<a href="http://www.easydarwin.org" target="_blank" title="EasyDarwin开源流媒体服务器">http://www.easydarwin.org</a><br/>
© TSINGSEE视频开放平台：<a href="http://open.tsingsee.com" target="_blank" title="TSINGSEE青犀视频开放平台">http://open.tsingsee.com</a><br/>

- 视频云服务：<br/>
© EasyDSS互联网视频云服务：<a href="http://www.easydss.com" target="_blank" title="EasyDSS互联网视频云服务">http://www.easydss.com</a><br/>
© EasyCVR安防视频云服务：<a href="http://www.easycvr.com" target="_blank" title="EasyCVR安防视频云服务">http://www.easycvr.com</a><br/>
© EasyGBS国标视频云服务：<a href="http://www.easygbs.com" target="_blank" title="EasyGBS国标视频云服务">http://www.easygbs.com</a><br/>
© EasyRTC在线视频会议平台：<a href="http://www.easyrtc.cn" target="_blank" title="EasyRTC在线视频会议平台">http://www.easyrtc.cn</a><br/>
© EasyRTS即时通信云服务：<a href="http://www.easyrts.com" target="_blank" title="EasyRTS即时通信云服务">http://www.easyrts.com</a><br/>

- 边缘计算：<br/>
© EasyNVR视频边缘计算网关：<a href="http://www.easynvr.com" target="_blank" title="EasyNVR视频边缘计算网关">http://www.easynvr.com</a><br/>
© EasyNTS上云网关：<a href="http://www.easynts.com" target="_blank" title="EasyNTS上云网关">http://www.easynts.com</a><br/>

© TSINGSEE Team：<a href="http://www.tsingsee.com" target="_blank" title="青犀TSINGSEE">http://www.tsingsee.com</a><br/>

![青犀TSINGSEE](http://www.easydarwin.org/public/images/tsingsee_qrcode_160.jpg)

