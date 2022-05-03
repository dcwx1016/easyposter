<template>
	<view class="home">
		<div class="header large-title">我要做</div>
		<div class="main-content">
			<button class="home-button title1" @click="handleJump">
				每日简报
			</button>
		</div>
		<text class="home-info footnote">其他功能还在闭关修炼中…\n如果你有任何建议/想法，欢迎来找我们！\n公众号：哎我就试一下</text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			onShareAppMessage(){
			},
			handleJump(){
				uni.navigateTo({url:"/pages/home/home"})
			},
			onLoad(){
				// wx.cloud.init({
				//   env: 'sbg-test-0gydry6z18aaa016'
				// });
				// const db = wx.cloud.database();
				// const feedback = db.collection('feeback');
				// feedback.add({
				//   // data 字段表示需新增的 JSON 数据
				//   data: {
				// 	// _id: 'todo-identifiant-aleatoire', // 可选自定义 _id，在此处场景下用数据库自动分配的就可以了
				// 	description: "test02"
				//   },
				//   success: function(res) {
				// 	// res 是一个对象，其中有 _id 字段标记刚创建的记录的 id
				// 	console.log(res)
				//   },
				//   fail: function(res) {
				// 	// res 是一个对象，其中有 _id 字段标记刚创建的记录的 id
				// 	console.log(res)
				//   }
				// })
			}
		}
	}
</script>

<style lang="scss">
.home, .main-content, .home-button, .home-info{
	display: flex;
	align-items: center;
}
.home{
	flex-direction: column;
	height: 100vh;
}
.header{
	margin-top: 64px;
}
.main-content{
	flex:1;
}
.home-button{
	width: 240px;
	height: 82px;
	background-color: #FFC700;
	border-radius: 48px;
	text-align: center;
	justify-content: center;
	&::after{
		border: none;
	}
}
.home-info{
	justify-content: center;
	text-align: center;
	margin-bottom: 64px;
}
</style>
