# uni-app 二维码生成器
### 作者：诗小柒

1. H5、微信小程序、支付宝小程序、APP，其它平台的小程序没有测试
2. 使用canvas生成  
3. 可设置二维码背景色，前景色，角标色  
4. 可设置二维码logo  

## 重要的事情说3遍 重要的事情说3遍 重要的事情说3遍

1. IOS、Android真机都可以正常生成二维码
2. 使用的时候出现无法生成二维码或空白的请先github直接打包下载，问题依旧，请github上直接提出问题并配图
3. 有问题请说明问题原因，这样我才好定位，否则我也无法解决
4. 如果此插件有帮助到你请打5分或赞赏我，你的支持是我更新的动力

+ 图片1 是微信小程序真机实测
+ 图片2 是微信小程序模拟实测
+ 图片3 是支付宝小程序模拟器实测
+ 图片4 是安卓真机实测
+ 图片5 H5

## 开始使用
NPM 
```
npm i tki-qrcode
```
GIT 
```
git clone https://github.com/q310550690/uni-app-qrcode
```

### 更新说明
* 0.1.7 修复支付宝无法生成的问题（导致这个问题是uni-app官方的template编译器没有编译出支付宝识别的canvas组件）
* 0.1.6 新增cid属性，支持同一个页面使用多个二维码组件
* 0.1.5 新增showLoading、loadingText属性
* 0.1.4 新增usingComponents属性，修复非自定义组件下 v-if 无法生成二维码的问题（非自定义组件下设置为false）
* 0.1.3 新增unit属性
* 0.1.2 适配新版uni-app编译器 感谢 "DCloud_UNI_Trust" (如果github上下载后使用新版HbuilderX1.7.1.20190320编译后无法启动请等待Dcloud更新即可)
* 0.1.1 新增监听val值变化时自动生成二维码(onval)、新增组件初始化时自动生成二维码(loadMake) 属性，具体说明看文档说明
* 0.1.0 常规更新
* 0.0.9 修复小程序真机生成二维码错乱问题（其实这是小程序canvas的锅）
* 0.0.8 修复官方 uni.canvasToTempFilePath 在有些平台返回字段不统一而导致的支付宝无法生成二维码的问题。
* 0.0.7 常规修复
* 0.0.6 新增角标色、二维码logo

### 使用方法
在 `script` 中引入组件
``` javascript
import tkiQrcode from "@/components/tki-qrcode/tki-qrcode.vue"
export default {
    components: {tkiQrcode}
}
```
在 `template` 中使用
``` javascript
<view class="qrimg">
    <tki-qrcode
    ref="qrcode"
    :cid="cid"
    :val="val"
    :size="size"
    :unit="unit"
    :background="background"
    :foreground="foreground"
    :pdground="pdground"
    :icon="icon"
    :iconSize="iconsize"
    :lv="lv" 
    :onval="onval"
    :loadMake="loadMake"
    :usingComponents="usingComponents"
    :showLoading="showLoading"
    :loadingText="loadingText"
    @result="qrR" />
</view>
```
### 属性

|属性名|类型|默认值|可选值|说明|
|:-|:-:|:--:|:--:|-:|
|cid|String|tki-qrcode-canvas| |canvasId，页面存在多个二维码组件时需设置不同的ID|
|size|Number|200| |生成的二维码大小|
|unit|String|upx|px|大小单位尺寸|
|show|Boolean|true| |默认使用组件中的image标签显示二维码|
|val|String|二维码| |要生成的内容|
|background|String|#000000| |二维码背景色|
|foreground|String|#ffffff| |二维码前景色|
|pdground|String|#ffffff| |二维码角标色|
|icon|String| | |二维码图标URL（必须是本地图片，网络图需要先下载至本地）|
|iconSize|Number|40<br/>注意此大小不会跟随二维码size 动态变化，设置时需注意大小，不要太大，以免无法识别| |二维码图标大小|
|lv|Number|3（一般不用设置）| |容错级别|
|onval|Boolean|false| |监听val值变化自动重新生成二维码|
|loadMake|Boolean|false| |组件初始化完成后自动生成二维码，val需要有值|
|usingComponents|Boolean|true| false |是否使用了自定义组件模式（主要是为了修复非自定义组件模式时 v-if 无法生成二维码的问题）|
|showLoading|Boolean|true| false |是否显示loading|
|loadingText|String|二维码生成中| |loading文字|

### 方法
|方法名|参数|默认值|说明|
|:-|:-:|:--:|-:|
|_makeCode()| | |生成二维码|
|_clearCode()| | |清空二维码（清空二维码会触发result回调 返回值为空）|
|_saveCode()| | |保存二维码到图库|

### 事件
|事件名|返回值|说明|
|:-|:-:|-:|
|result|生成的图片base64或图片临时地址|返回二维码路径 注：_clearCode()后返回空|


### 感谢

[uni-app](https://uniapp.dcloud.io/ "uni-app")
[qrcode](https://github.com/aralejs/qrcode "qrcode")