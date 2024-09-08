# 媒体流合并、录制、下载

## Demo
![效果](https://github.com/gws0920/video-stream/blob/master/public/demo.png)

## 故障排查
- https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getDisplayMedia#examples
  - https://screen-sharing-controls.glitch.me/

桌面音频音质差
```js
// ref https://stackoverflow.com/a/67694841/16834604
var constraints = { channelCount: 2, noiseSuppression: false, autoGainControl: false, }
// echoCancellation 有时候会出问题，得具体测试不同的浏览器版本
var screen = await navigator.mediaDevices.getDisplayMedia({ video: true, audio: constraints })
```

另外，Chrome `128.0.6613.120` 左右的几个版本都不行

找了一下最开始兼容 macOS `ScreenCaptureKit` 新 API 的这个 [pr](https://chromium-review.googlesource.com/c/chromium/src/+/4774561) 在 Sep 20, 2023 提出的，以及[设计方案](https://docs.google.com/document/d/1v-or4bSTeBjnO5nQe4lNRWtSBAOjD-7coYgqSucg1mU)

然后找了个距离这个 PR 最近发布的版本，测试是可以用的。[macOS Arm 直达链接](https://commondatastorage.googleapis.com/chromium-browser-snapshots/index.html?prefix=Mac_Arm/1204255/)

Chromium: 119，build number: 1204255，filename: Mac_Arm_1204255_chrome-mac

我的机子
```
Chromium	119.0.6045.0 (Developer Build) (arm64) 
Revision	9eb86394783fcb977e205ef57fab54c47f79f35c-refs/heads/main@{#1204255}
OS	macOS Version 14.5 (Build 23F79)
JavaScript	V8 11.9.169
User Agent	Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36
```


## 项目启动
```
yarn
yarn dev
```
## 框架
- vue 3.0
## 脚手架
- vite 2.6
## 媒体流合并
- video-stream-merger
## 媒体流录制
- MediaRecorder
