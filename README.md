# EasyPlayer.js

## 简介

集播放http-flv, rtmp, hls, websocket 于一身的H5`视频直播/视频点播`播放器, 使用简单, 功能强大；

## 功能说明

- [x] 支持 MP4 播放

- [x] 支持 m3u8/HLS 播放;

- [x] 支持 HTTP-FLV/WS-FLV 播放;

- [x] 支持 RTMP 播放;

- [x] 支持直播和点播播放;

- [x] 支持播放器快照截图;

- [x] 支持点播多清晰度播放;

- [x] 支持全屏或比例显示;

- [x] 自带的 flash 支持极速和流畅模式;

- [x] 自带的 flash 支持 HTTP-FLV 播放;

- [x] 自动检测 IE 浏览器兼容播放;

- [x] 支持重连播放；

## HTML 集成示例

- 使用方式

- [x] 普通集成

copy dist/element/EasyPlayer-element.min.js 到 www 根目录

在 html 中引用 dist/element/EasyPlayer-element.min.js

```html
<!DOCTYPE html>
<html>
  <head>
    <title>liveplayer</title>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta
      content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no"
      name="viewport"
    />
    <script type="text/javascript" src="EasyPlayer-element.min.js"></script>
  </head>
  <body>
    <easy-player
      video-url="rtmp://live.hkstv.hk.lxdns.com/live/hks2"
      live="true"
      stretch="true"
    ></easy-player>
    <easy-player
      video-url="http://live.hkstv.hk.lxdns.com/live/hks/playlist.m3u8"
      live="false"
      stretch="true"
    ></easy-player>
    <easy-player
      video-url="http://live.hkstv.hk.lxdns.com/flv/hks.flv"
      live="true"
      stretch="true"
    ></easy-player>
  </body>
</html>
```

- [x] vue集成

```
  npm install @easydarwin/easyplayer --save
```

- Vue 集成调用

copy node_modules/@easydarwin/easyplayer/dist/component/EasyPlayer.swf 到 静态文件 根目录

copy node_modules/@easydarwin/easyplayer/dist/component/crossdomain.xml 到 静态文件 根目录

copy node_modules/@easydarwin/easyplayer/dist/component/EasyPlayer-lib.min.js 到 静态文件 根目录

**注意：** 没有调用会出现无法加载对应插件的报错

在 html 中引用 dist/component/EasyPlayer-lib.min.js

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
    <script src="./EasyPlayer-lib.min.js"></script>
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

##效果演示

![](http://www.easydarwin.org/github/images/easyplayer/easyplayer.js/easyplayer.js.20190923.png)

- [x] npm集成

```html
......

<EasyPlayer
  :videoUrl="videoUrl"
  :aspect="aspect"
  live
  @message="$message"
  :fluent="fluent"
  :autoplay="autoplay"
  stretch
></EasyPlayer>

...... ...... import EasyPlayer from '@easydarwin/easyplayer'; ......
components: { EasyPlayer }
```

源码演示：[github-demo](https://github.com/EasyNVR/EasyNVR)

## 配置属性

| 参数               | 说明                                             | 类型                       | 默认值 |
| ------------------ | ------------------------------------------------ | -------------------------- | ------ |
| video-url          | 视频地址                                         | String                     | -      |
| video-title        | 视频右上角显示的标题                             | String                     | -      |
| snap-url           | 视频封面图片                                     | String                     | -      |
| auto-play          | 自动播放                                         | Boolean                    | true   |
| live               | 是否直播, 标识要不要显示进度条                   | Boolean                    | true   |
| speed              | 是否显示倍速播放按钮。注意：当live为true时，此属性不生效 |Boolean                | true   |
| loop               | 是否轮播。                                      |Boolean                | false  |
| alt                | 视频流地址没有指定情况下, 视频所在区域显示的文字 | String                     | 无信号 |
| muted              | 是否静音                                         | Boolean                    | false  |
| aspect             | 视频显示区域的宽高比                             | String                     | 16:9   |
| isaspect           | 视频显示区域是否强制宽高比                       | Boolean                    | true   |
| loading            | 指示加载状态, 支持 sync 修饰符                   | String                     | -      |
| fluent             | 流畅模式                                         | Boolean                    | true   |
| timeout            | 加载超时(秒)                                     | Number                     | 20     |
| stretch            | 是否不同分辨率强制铺满窗口                       | Boolean                    | false  |
| show-custom-button | 是否在工具栏显示自定义按钮(极速/流畅, 拉伸/标准) | Boolean                    | true   |
| isresolution       | 是否在播放 m3u8 时显示多清晰度选择               | Boolean                    | false  |
| isresolution       | 供选择的清晰度 "yh,fhd,hd,sd", yh:原始分辨率     | fhd:超清，hd:高清，sd:标清 | -      |
| resolutiondefault  | 默认播放的清晰度                                 | String                     | hd     |

### HTTP-FLV 播放相关属性
#### 注意：此属性只在播放flv格式的流时生效。
| 属性     | 说明                                   | 类型    | 默认值             |
| -------- | -------------------------------------- | ------- | ------------------ |
| hasaudio | 是否有音频，传递该属性可以加快启播速度 | Boolean | 默认不配置自动判断 |
| hasvideo | 是否有视频，传递该属性可以加快启播速度 | Boolean | 默认不配置自动判断 |

## 事件回调

| 方法名     | 说明         | 参数                  |
| ---------- | ------------ | --------------------- |
| video-url  | 触发通知消息 | type: '', message: '' |
| ended      | 播放结束     | -                     |
| timeupdate | 进度更新     | 当前时间进度          |
| pause      | 暂停         | 当前时间进度          |
| play       | 播放         | 当前时间进度          |


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

