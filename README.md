# EasyPlayer

## 简介

> 集 flv.js, rtmp, hls, websocket 于一身的`网页直播/点播`播放器, 使用简单, 功能强大

## 功能说明

支持 MP4 播放

支持 m3u8/HLS 播放;

支持 HTTP-FLV/WS-FLV 播放;

支持 RTMP 播放;

支持直播和点播播放;

支持播放器快照截图;

支持点播多清晰度播放;

支持全屏或比例显示;

自带的 flash 支持极速和流畅模式;

自带的 flash 支持 HTTP-FLV 播放;

自动检测 IE 浏览器兼容播放;

## HTML 集成示例

- 安装

```
  npm install @easydarwin/easyplayer --save
```

- Vue 集成调用

copy node_modules/@easydarwin/easyplayer/dist/component/EasyPlayer.swf 到 静态文件 根目录

copy node_modules/@easydarwin/easyplayer/dist/component/crossdomain.xml 到 静态文件 根目录

copy node_modules/@easydarwin/easyplayer/dist/component/EasyPlayer-lib.min.js 到 静态文件 根目录

**注意：** 没有调用会出现无法加载对应插件的报错

在 html 中引用 dist/component/easy-player-lib.min.js

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
    <script src="./easy-player-lib.min.js"></script>
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

- 脱离 Vue 使用

copy dist/element/easy-player-element.min.js 到 www 根目录

在 html 中引用 dist/element/easy-player-element.min.js

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
    <script type="text/javascript" src="liveplayer-element.min.js"></script>
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

##效果演示

![](http://ww1.sinaimg.cn/large/79414a05gy1fmpjkmmm57j20cz0lutjj.jpg)

## 配置属性

| 参数               | 说明                                             | 类型                       | 默认值 |
| ------------------ | ------------------------------------------------ | -------------------------- | ------ |
| video-url          | 视频地址                                         | String                     | -      |
| video-title        | 视频右上角显示的标题                             | String                     | -      |
| snap-url           | 视频封面图片                                     | String                     | -      |
| auto-play          | 自动播放                                         | Boolean                    | true   |
| live               | 是否直播, 标识要不要显示进度条                   | Boolean                    | true   |
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
