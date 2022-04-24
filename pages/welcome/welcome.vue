<template>
	<view class="attainShare">
	  <view class="canvasCss">
		<painter :palette="paintPallette" @imgOK="onImgOK" :use2D="true"/>
	  </view>
	  <view class="canvasButton" >
		<button type="default" @click="saveImage">保存图片</button>
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
					content:'北门已全面封闭，请联系外卖员到南门送货。将有专业人士对货品进行消杀处理；明日核酸，请居民提前做好准备；小区巡逻队已成立，请居民继续保持“足不出户”。',
					contact:'如有疑问请联系张三 139XXXXXXXX',
					date: '2022年4月14日'
				};
				let views = [];
				views.push({
					type: 'rect',
					css: {
					  left: '16px',
					  top: '77px',
					  color:'#FAFAFA',
					  width: '312px',
					  height:'229px',
					  borderRadius: '16px'
					},
				});
				views.push({
					type: 'text',
					text: data.title,
					css: {
					  left: '16px',
					  top: '16px',
					  fontSize: '24px',
					  lineHeight: '29px',
					  fontFamily: 'Inter',
					  fontWeight: 600,
					},
				});
				views.push({
					type: 'text',
					text: data.date,
					css: {
					  left: '16px',
					  top: '49px',
					  fontSize: '14px',
					  lineHeight: '20px',
					  fontFamily: 'Inter',
					  fontWeight: 600,
					},
				});
				views.push({
					type: 'text',
					text: '公告',
					css: {
					  left: '156px',
					  top: '89px',
					  fontSize: '16px',
					  lineHeight: '22px',
					  fontFamily: 'Inter',
					  fontWeight: 600,
					},
				});
				views.push({
					type: 'text',
					text: data.content,
					css: {
					  left: '32px',
					  top: '123px',
					  fontWeight: 400,
					  fontSize: '16px',
					  fontFamily: 'Inter',
					  lineHeight: '24px',
					  width: '280px'
					},
				});
				views.push({
					type: 'image',
					url: data.imgUrl ? data.imgUrl[0] : 'http://tmp/YIMSNIHfEZOca8909a9935ba9f95aaab9aca11f20798.jpeg',
					css: {
					  left: '16px',
					  top: '314px',
					  mode: "aspectFill",
					  width: '312px',
					  height: '180px'
					},
				});
				views.push({
					type: 'text',
					text: data.contact,
					css: {
					  right: '14px',
					  bottom: '14px',
					  fontWeight: 400,
					  fontSize: '12px',
					  lineHeight: '22px',
					  color: 'black'
					},
				});

				this.paintPallette = {
				  width: '344px',
				  height: '539px',
				  background: '#fff',
				  views: views,
				}
			},
	}}
</script>

<style lang="scss">
.canvasCss{
	display: flex;
	justify-content: center;
	margin: 12px;
	border: 1px solid black;
}
.canvasButton{
	display: flex;
	justify-content: center;
	margin-top: 40px;
	& button{
		font-family: 'Inter';
		font-style: normal;
		font-weight: 600;
		font-size: 18px;
		line-height: 25px;
		display: flex;
		justify-content: center;
		align-items: center;
		text-align: center;
		width: 120px;
		height: 48px;
		background: #FFC700;
		border-radius: 48px;
		&::after{
			border: none;
		}
	}
}
</style>
