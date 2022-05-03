<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	/*每个页面公共css */
	@import '/wxcomponents/vant/common/index.wxss';
	/* 字体参考
LargeTitle：PingFang SC、字号34、行高41、Semibold
Title1：PingFang SC、字号22、行高28、Semibold
Title2：PingFang SC、字号22、行高28、Regular
Title3：PingFang SC、字号17、行高23、Semibold
Subtitle：PingFang SC、字号15、行高20、Regular
Footnote：PingFang SC、字号13、行高18、Regular、40%
ps：当前部分字体为inter */
	*{
		font-family: PingFang SC;
	}
	.large-title{
		font-size: 34px;
		font-weight: 600;
		line-height: 41px;
		text-align: center;
	}
	.title1{
		font-size: 22px;
		font-weight: 600;
		line-height: 28px;
	}
	.title2{
		font-size: 22px;
		font-weight: 400;
		line-height: 28px;
	}
	.title3{
		font-size: 17px;
		font-weight: 600;
		line-height: 23px;
	}
	.subtitle{
		font-size: 15px;
		font-weight: 400;
		line-height: 20px;
	}
	.footnote{
		font-size: 13px;
		font-weight: 400;
		line-height: 18px;
		color: #969696;
	}
</style>
