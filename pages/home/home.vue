<template>
	<view class="content">
		<view class="main">
			<view class="header">
				<text class='title'>小区日报</text>
				<text class="subtitle">输入信息将展示在日报中</text>
			</view>
			<scroll-view :scroll-y="true" :style="{'height':scrollViewH}" scroll-with-animation="true">
				<view class="input-block">
					<text>日报的时间</text>
					<van-cell custom-class='test' @click="showPopup(true)">
						<view slot="title" style="font-size: 14px;color: rgba(0,0,0,.4)">
							{{date}}
						</view>
					</van-cell>
				</view>
				<view class="input-block">
					<text>小区名字</text>
					<textarea 
						class='test'
						placeholder="例：万达城市公寓" 
						placeholder-style="font-size: 14px;color: rgba(0,0,0,.4);"
						v-model="title" 
						@change='onChangeTitle'
					/>
	<!-- 				<text class="length">
						{{ title.length }}/10
					</text> -->
				</view>
				<view class="input-block">
					<text>公告</text>
					<textarea 
						class='test-multi'
						placeholder-style="font-size: 14px;color: rgba(0,0,0,.4)"
						placeholder="简要阐明公告内容，建议不超过3点" 
						v-model="content" 
						@change='onChangeContent'/>
	<!-- 				<text class="length">
						{{ content.length }}/50
					</text> -->
				</view>
				<view class="input-block" v-if="!imgUrl">
					<text>上传你的小区平面图</text>
					<view class='img-upload' >
						<text @click="ChooseImage">
							可先编辑后上传
						</text>
					</view>
				</view>
				<view class="input-block" v-else>
					<text>上传你的小区平面图</text>
					<view class="image-preview">
						<view style="width:100px;position: relative;">
							<image :src="imgUrl" mode="aspectFit"/>
							<i @click="removeImg" class="iconfont icon-shanchu"></i>
						</view>
					</view>
				</view>
				<view class="input-block">
					<text>备注</text>
					<textarea 
						class='test'
						placeholder-style="font-size:14px;color: rgba(0,0,0,.4)"
						placeholder="例：张三 139xxxxxxxx" 
						v-model="contact" 
						@change='onChangeContact'
					/>
				</view>		
			</scroll-view>
		</view>
		<view class="create-poster">
			<button type="default" @click="handleCreate">生成</button>
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
				date: 'YYYY/MM/DD',//日期
				show: false,				
			}
		},
		methods: {
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