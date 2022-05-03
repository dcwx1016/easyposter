<template>
	<view class="attainShare">
	  <view class="canvasCss">
		  <image :src="imagePath" mode="scaleToFill"/>
	  </view>
	  <view class="canvasButton" >
		<button class="title3" type="default" @click="saveImage">保存</button>
	  </view>
	  <view style="position:fixed;left:-9999px">
	  	<painter :palette="paintPallette" @imgOK="onImgOK" widthPixels="720" :use2D="true"/>
	  </view>
	</view>
</template>

<script>
	import Text from './palette/text-example';
	
	export default {
		data() {
			return {
				imagePath: '',
				isSave: false,
				paintPallette: null,
				temp: null,
			}
		},
		methods: {
			onShareAppMessage() {
			},
			onImgOK(e) {
			  this.imagePath = e.detail.path;
			  if (this.isSave) {
			    this.saveImage(this.imagePath);
			  }
			},
			saveImage() {
				if (this.imagePath && typeof this.imagePath === 'string') {
					this.isSave = false;
					wx.saveImageToPhotosAlbum({
					  filePath: this.imagePath,
					}).then((res)=>{
						uni.showToast({
							title: '保存成功',
							duration: 2000
						});
					}).catch((err)=>{
						this.handleAuthorize();
					});
				}
			},
			handleAuthorize(){
				wx.getSetting({ 
					success(res){
					  const writePhotosAlbum = res.authSetting['scope.writePhotosAlbum']
					  if(!writePhotosAlbum) { //检查用户是否授权了保存图片，没有则引导授权
						wx.showModal({
							content:'是否打开权限设置',
							success: function(res){
								uni.openSetting()
							}
						})
					  }
					}
				  })
			},
			onLoad(option){
				let data = option.views ? JSON.parse(decodeURIComponent(option.views)) : {
					title:'万达城市公寓',
					content:'北门已全面封闭，请联系外卖员到南门送货。将有专业人士对货品进行消杀处理；明日核酸，请居民提前做好准备；小区巡逻队已成立，请居民继续保持“足不出户”。将有专业人士对货品进行消杀处理；明日核酸，请居民提前做好准备；',
					contact:'如有疑问请联系张三 139XXXXXXXX',
					date: '2022年4月14日'
				};
				let views = [];
				views.push({
					type: 'rect',
					css: {
					  left: '32px',
					  top: '138px',
					  color:'#EFEFEF',
					  width: '486px',
					  height:'762px',
					},
				});
				views.push({
					type: 'rect',
					css: {
					  left: '22px',
					  top: '128px',
					  color:'#FFFFFF',
					  width: '486px',
					  height:'762px',
					},
				});
				views.push({
					type: 'rect',
					css: {
					  left: '22px',
					  top: '108px',
					  color:'#538BDE',
					  width: '126px',
					  height:'40px',
					  borderRadius: '8px'
					},
				});
				views.push({
					type: 'text',
					text: data.title,
					css: {
					  left: '20px',
					  top: '24px',
					  fontSize: '30px',
					  lineHeight: '42px',
					  fontFamily: 'PingFang SC',
					  fontWeight: 600,
					},
				});
				views.push({
					type: 'text',
					text: '发布于 '+data.date,
					css: {
					  left: '20px',
					  top: '70px',
					  fontSize: '16px',
					  lineHeight: '22px',
					  fontFamily: 'PingFang SC',
					  fontWeight: 400,
					},
				});
				views.push({
					type: 'text',
					text: '公告',
					css: {
					  left: '67px',
					  top: '116px',
					  fontSize: '18px',
					  lineHeight: '25px',
					  fontFamily: 'PingFang SC',
					  fontWeight: 500,
					  color: '#FFFFFF'
					},
				});
				views.push({
					type: 'text',
					text: data.content,
					css: {
					  left: '55px',
					  top: '166px',
					  fontWeight: 400,
					  fontSize: '16px',
					  fontFamily: 'PingFang SC',
					  lineHeight: '22.4px',
					  width: '420px'
					},
				});
				views.push({
					type: 'text',
					text: data.contact,
					css: {
					  right: '24px',
					  bottom: '16px',
					  fontFamily: 'PingFang SC',
					  fontWeight: 400,
					  fontSize: '14px',
					  lineHeight: '20px',
					  color: '#000000'
					},
				});
				var _this = this;
				if(data.imgUrl && data.imgUrl[0]){
					uni.getImageInfo({
						src:data.imgUrl[0],
						success:function(img){
							console.log(img.width, img.height);
							if(img.width > img.height){
								let t = 432 + (420 - img.height*420/img.width)/2 + 'px';
								let h = img.height*420/img.width + 'px';
								views.push({
									type: 'image',
									url: data.imgUrl[0],
									css: {
									  left: '55px',
									  top: t,
									  width: '420px',
									  height: h
									},
								});
								_this.paintPallette = {
								  width: '540px',
								  height: '960px',
								  background: '#F7F8F9',
								  views: views,
								}
							}else{
								let t = (540 - img.width*420/img.height)/2 + 'px';
								let w = img.width*420/img.height + 'px';
								views.push({
									type: 'image',
									url: data.imgUrl[0],
									css: {
									  left: t,
									  top: '432px',
									  width: w,
									  height: '420px'
									},
								});
								_this.paintPallette = {
								  width: '540px',
								  height: '960px',
								  background: '#F7F8F9',
								  views: views,
								}
							}
						}
					})
				}else{
					this.paintPallette = {
					  width: '540px',
					  height: '960px',
					  background: '#F7F8F9',
					  views: views,
					}
				}
			},
	}}
</script>

<style lang="scss">
.canvasCss{
	display: flex;
	justify-content: center;
	background-color: #F7F8F9;
	margin: 24px;
	border: 0.5px solid black;
	image{
		width: 327px; 
		height:560px
	}
}
.canvasButton{
	display: flex;
	justify-content: center;
	margin-top: 40px;
	& button{
		display: flex;
		justify-content: center;
		align-items: center;
		text-align: center;
		width: 240px;
		height: 48px;
		background: #FFC700;
		border-radius: 48px;
		&::after{
			border: none;
		}
	}
}
</style>
