<template>
	<view class="content">
		<scroll-view :scroll-y="true">
			<view class="main">
				<view class="input-block">
					<text class="title3">你想在哪里发布？</text>
					<van-field custom-class='block' placeholder="请填写小区、街道或弄堂名称" @change="changeTitle"/>
				</view>
				<view class="input-block">
					<text class="title3">你想在哪天发布？</text>
					<van-cell custom-class='block' @click="showPopup(true)">
						<view slot="title" style="color: #969696;font-size: 13px;">
							{{date}}
						</view>
					</van-cell>
				</view>
				<view class="input-block">
					<text class="title3">你想告诉大家什么内容？</text>
					<textarea 
						class='block multi footnote'
						placeholder-style="font-size: 13px;color: #969696"
						placeholder="请简要阐明需要通知的内容:" 
						maxlength="200"
						v-model="content"/>
				</view>
				<view class="input-block" v-if="!imgUrl">
					<text class="title3">你想上传小区平面图/信息图吗？</text>
					<view class='block img-upload' >
						<text class="footnote" @click="ChooseImage">
							可在预览中选择编辑图片，并标记重要信息
						</text>
					</view>
				</view>
				<view class="input-block" v-else>
					<text class="title3">你想上传小区平面图/信息图吗？</text>
					<view class="image-preview">
						<view style="width:100px;position: relative;">
							<image :src="imgUrl" mode="aspectFit"/>
							<i @click="removeImg" class="iconfont icon-shanchu"></i>
						</view>
					</view>
				</view>
				<view class="input-block">
					<text class="title3">你还想补充什么呢？</text>
					<van-field custom-class='block' placeholder="可填写负责人及其联系方式，或你想说的话" @change="changeContact"/>
				</view>		
				</view>
		</scroll-view>
		
		<view class="create-poster">
			<button class="title3" type="default" @click="handleCreate">生成简报</button>
		</view>
		<van-calendar :show="show" :show-confirm="false" @close="showPopup(false)" @confirm="onConfirm"/>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '', //小区名字
				content: '',//公告内容
				contact: '',//备注
				imgUrl: '',//图片
				date: '请点击并选择具体日期',//日期
				show: false,				
			}
		},
		methods: {
			onShareAppMessage(){
			},
			changeTitle(val){
				this.title = val.detail;
			},
			changeContact(val){
				this.contact = val.detail;
			},
			handleCreate(){
				let t = JSON.stringify({
					title: this.title, //小区名字
					content: this.content,//公告内容
					contact: this.contact,//备注
					imgUrl: this.imgUrl,//图片
					date: this.date//日期
				});
				uni.navigateTo({  
				    url: '/pages/welcome/welcome?views=' + encodeURIComponent(t)
				});
			},
			removeImg(){
				this.imgUrl = "";
			},
			ChooseImage(){
				uni.chooseImage({
					count: 1, //图片数量
					sizeType: ['compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album','camera'], //从相册选择
					success: (res) => {
						this.imgUrl = res.tempFilePaths;
						console.log(this.imgUrl);
					}
				});
			},
			onConfirm(event){
				let t = new Date(event.detail);
				this.date = `${t.getYear() + 1900}年${t.getMonth() + 1}月${t.getDate()}日`;
				this.show = false;
			},
			showPopup(val){
				this.show = val;
			},
		}
	}
</script>

<style lang="scss">
	@import "../icon.scss";
	@import './home.scss';
	::-webkit-scrollbar {
		display: none;
	}
</style>