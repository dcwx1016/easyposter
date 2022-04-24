<template>
	<view class="home">
		<div class="home-title">我要做</div>
		<button class="home-button" @click="handleJump">
			小区简报
		</button>
		<text class="home-info">其他功能敬请期待...</text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			handleJump(){
				uni.navigateTo({url:"/pages/home/home"})
			}
		}
	}
</script>

<style lang="scss">
.home{
	display: flex;
	flex-direction: column;
	justify-content: space-around;
	height: 100vh;
}
.home-title{
	font-family: PingFang SC;
	font-size: 36px;
	font-weight: 600;
	line-height: 50px;
	letter-spacing: 0em;
	text-align: center;
}
.home-button{
	width: 240px;
	height: 82px;
	background-color: #FFC700;
	border-radius: 48px;
	font-family: PingFang SC;
	font-size: 24px;
	font-weight: 600;
	line-height: 34px;
	letter-spacing: 0em;
	display: flex;
	justify-content: center;
	align-items: center;
	text-align: center;
	&::after{
		border: none;
	}
}
.home-info{
	font-family: 'Inter';
	font-style: normal;
	font-weight: 400;
	font-size: 14px;
	line-height: 17px;
	display: flex;
	justify-content: center;
	align-items: center;
	text-align: center;
}
</style>
