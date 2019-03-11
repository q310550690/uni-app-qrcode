# uni-app 二维码生成器
### 作者：诗小柒

1.H5、微信小程序、支付宝小程序、APP，其它平台的小程序没有测试
2.使用canvas生成  
3.可设置二维码背景色，前景色，角标色  
4.可设置二维码logo  
5.不懂如何使用可以去[github](https://github.com/q310550690/uni-app-qrcode)直接打包下载运行  
## 声明
此程序我测试在 xzp8.0 xzp9.0 真机上通过，没有出现问题,H5 测试了好几台手机也都是正的，小程序真机测试也是正常的，IOS设备没有测试过，因为我不用苹果的东西，周围也没有什么人在用，所以无法测试，在使用次程序时产生的问题可以先去github 直接打包下载运行看看，如果还是不行请直接在 github 提交问题，最好配图，我好定位问题所在，还有就是，最近身体转态不是很好，可能也不会太上心这些插件了，出问题了又急用的可以自己看下源代码改下，多数都有中文注释的，谢谢
## 开始使用

npm i tki-qrcode
或
https://github.com/q310550690/uni-app-qrcode 
### 0.更新说明
修复官方 uni.canvasToTempFilePath 在有些平台返回字段不统一而导致的支付宝无法生成二维码的问题。
### 1.引入组件
```javascript
// template 使用
<tki-qrcode :val="qrval" :size="qrsize" :background="qrbackground" :foreground="qrforeground" :pdground="qrpdground" :icon="qricon" :iconSize="qriconsize" :lv="qrlv" ref="qrcode" @result="qrR"></tki-qrcode>

// 普通引入组件
import tkiQrcode from '@/components/tki-qrcode/tki-qrcode.vue'
// npm引入
import tkiQrcode from "tki-qrcode"
// 注册组件
components: {
    tkiQrcode
},
```

### 2.属性
`size` Number
```
size 生成的二维码大小  默认值：200
```
`show` Boolean
```
show 默认使用组件中的image标签显示二维码  默认值：true
```
`val` String
```
val 要生成的内容  默认值：
```
`background` String 
```
background 二维码背景色   默认值：#000000
```
`foreground` String 
```
foreground 二维码前景色   默认值：#ffffff
```
`pdground` String 
```
pdground 二维码角标色   默认值：#ffffff
```
`icon` String 
```
icon 二维码图标URL   默认值：空
```
`iconSize` Number 
```
iconSize 二维码图标大小   默认值：40   注意此大小不会跟随二维码size 动态变化，设置时需注意大小，不要太大，以免无法识别
```
`lv` Number 
```
lv 容错级别   默认值：3   一般不用设置
```

### 3.方法
`_makeCode()` Function
```
_makeCode() 生成二维码
```
`_clearCode()` Function
```
_clearCode() 清空二维码 注:清空二维码会触发result回调 返回值为空
```
`_saveCode()` Function
```
_saveCode() 保存二维码到图库
```

### 4.回调
`result` Function
```
@result="resultFn" 返回二维码路径 注：_clearCode()后返回空
```

### 5.问题
暂无问题

### 6.感谢

[uni-app](https://uniapp.dcloud.io/ "uni-app")
[qrcode](https://github.com/aralejs/qrcode "qrcode")