<template xlang="wxml">
	<view class="container">
		<!-- <page-head :title="title"></page-head> -->
		<view class="qrimg">
			<tki-qrcode :val="qrval" :size="qrsize" :background="qrbackground" :foreground="qrforeground" :pdground="qrpdground" :icon="qricon" :iconSize="qriconsize" :lv="qrlv" ref="qrcode" @result="qrR"></tki-qrcode>
		</view>
		<view class="uni-padding-wrap">
			<view class="uni-title">请输入要生成的二维码内容</view>
		</view>
		<view class="uni-list">
			<view class="uni-list-cell">
				<input class="uni-input" placeholder="请输入要生成的二维码内容" :value="qrval" @input="bindClearInput" />
				<view class="uni-icon uni-icon-clear" v-if="showClearIcon" @click="clearIcon"></view>
			</view>
		</view>
		<view class="uni-padding-wrap uni-common-mt">
			<view class="uni-title">设置二维码大小</view>
		</view>
		<view class="body-view">
			<slider :value="qrsize" @change="sliderchange" min="50" max="500" show-value />
		</view>
		<view class="uni-padding-wrap">
			<view class="uni-btn-v uni-common-mt">
				<button type="primary" @tap="selectIcon">选择二维码图标</button>
				<button type="primary" @tap="creatQrcode">生成二维码</button>
				<button type="primary" @tap="saveQrcode">保存到图库</button>
				<button type="warn" @tap="clearQrcode">清除二维码</button>
			</view>
		</view>
		<!-- <page-foot :name="name"></page-foot> -->
	</view>
</template>
<script>
import tkiQrcode from '@/components/tki-qrcode/tki-qrcode.vue'
export default {
	data() {
		return {
			title: '二维码生成',
			name: '诗小柒',
			showClearIcon: false,
			qrval: '二维码', // 要生成的二维码值
			qrsize: 200, // 二维码大小
			qrbackground: '#b4e9e2', // 背景色
			qrforeground: '#309286', // 前景色
			qrpdground: '#32dbc6', // 角标色
			qricon: '', // 二维码图标
			qriconsize: 40, // 二维码图标大小
			qrlv: 3, // 二维码容错级别 ， 一般不用设置，默认就行
			qrSrc: ''
		}
	},
	methods: {
		bindClearInput: function (e) {
			this.qrval = e.target.value;
			if (e.target.value.length > 0) {
				this.showClearIcon = true;
			} else {
				this.showClearIcon = false;
			}
		},
		clearIcon: function () {
			this.qrval = "";
			this.showClearIcon = false;
		},
		sliderchange(e) {
			this.qrsize = e.detail.value
		},
		creatQrcode() {
			this.$refs.qrcode._makeCode()
		},
		saveQrcode() {
			this.$refs.qrcode._saveCode()
		},
		qrR(res) {
			this.qrSrc = res
		},
		clearQrcode() {
			this.$refs.qrcode._clearCode()
			this.clearIcon();
		},
		selectIcon() {
			let that = this
			uni.chooseImage({
				count: 1, //默认9
				sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
				sourceType: ['album'], //从相册选择
				success: function (res) {
					that.qricon = res.tempFilePaths[0]
					// console.log(res.tempFilePaths);
				}
			});
		}
	},
	components: {
		tkiQrcode
	}
}
</script>

<style>
/* @import "../../../common/icon.css"; */
.container {
  display: flex;
  flex-direction: column;
}
.qrimg {
  display: flex;
  justify-content: center;
}
slider {
  width: 100%;
}
</style>
