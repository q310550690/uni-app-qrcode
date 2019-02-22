<template xlang="wxml" minapp="mpvue">
	<view class="_qrCode">
		<canvas class="_qrCodeCanvas" id="_myQrCodeCanvas" canvas-id="_myQrCodeCanvas" :style="{width:cSize+'px',height:cSize+'px'}" />
		<image v-if="show" :src="result" :style="{width:cSize+'px',height:cSize+'px'}" />
	</view>
</template>

<script>
import QRCode from "./qrcode.js"
let qrcode
export default {
	name: "tki-qrcode",
	props: {
		size: {
			type: Number,
			default: 200
		},
		show: {
			type: Boolean,
			default: true
		},
		val: {
			type: String,
			default: ''
		},
		background: {
			type: String,
			default: '#000000'
		},
		foreground: {
			type: String,
			default: '#ffffff'
		},
		pdground: {
			type: String,
			default: '#ffffff'
		},
		icon: {
			type: String,
			default: ''
		},
		iconSize: {
			type: Number,
			default: 40
		},
		lv: {
			type: Number,
			default: 3
		},
	},
	data() {
		return {
			cSize: this.size,
			result: '',
		}
	},
	methods: {
		_makeCode() {
			let that = this
			qrcode = new QRCode({
				text: that.val, // 生成内容
				size: that.cSize, // 二维码大小
				background: that.background, // 背景色
				foreground: that.foreground, // 前景色
				pdground: that.pdground, // 定位角点颜色
				correctLevel: that.lv, // 容错级别
				image: that.icon, // 二维码图标
				imageSize: that.iconSize,// 二维码图标大小
				cbResult: function (res) { // 生成二维码的回调
					that._result(res)
				}
			});
		},
		_clearCode() {
			this._result('')
			qrcode.clear()
		},
		_saveCode() {
			let that = this;
			if (this.result != "") {
				uni.saveImageToPhotosAlbum({
					filePath: that.result,
					success: function () {
						uni.showToast({
							title: '二维码保存成功',
							icon: 'success',
							duration: 2000
						});
					}
				});
			}
		},
		_result(res) {
			this.result = res;
			this.$emit('result', res)
		}
	},
	computed: {
	},
	watch: {
		size: function (n, o) {
			if (n != o) {
				this.cSize = n
				setTimeout(() => {
					this._makeCode()
				}, 100);
			}
		}
	},
	onLoad: function () {
		// console.log(this.val)
	}
}
</script>
<style>
._qrCode {
  position: relative;
}
._qrCodeCanvas {
  position: fixed;
  top: -99999upx;
  left: -99999upx;
  z-index: -99999;
}
</style>
