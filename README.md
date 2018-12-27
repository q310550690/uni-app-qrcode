# uni-app 二维码生成器
### 作者：诗小柒


## 开始使用

npm i tk-qrcode
或
https://github.com/q310550690/uni-app-qrcode 

### 1.引入组件
```javascript
// template 使用
<qrcode :val="qrval" :size="qrsize" :colorDark="qrColorDark" :colorLight="qrColorLight" ref="qrcode" @result="qrR"></qrcode>

// 普通引入组件
import qrcode from '@/components/tkQrcode/tkQrcode.vue'
// npmy引入
import qrcode from "tk-qrcode"
// 注册组件
components: {
    qrcode
},
```

### 2.属性
`size` Number
```
size 生成的二维码大小  默认值：100
```
`show` Boolean
```
show 默认使用组件中的image标签显示二维码  默认值：true
```
`val` String
```
val 要生成的内容  默认值：
```
`colorDark` String 
```
colorDark 背景色   默认值：#000000
```
`colorLight` String 
```
colorLight 前景色   默认值：#ffffff
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
[weapp-qrcode](https://github.com/tomfriwel/weapp-qrcode "weapp-qrcode")