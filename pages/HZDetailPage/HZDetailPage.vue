<template>
	<view class="content">
		<view class="status-bar"></view>
		<view class="status-bar-zw"></view>
		<view class="nav-bar">
			<view class="nav-bar-backicon" @click="goback()">
				<image src="../../static/backIcon.png" mode=""></image>
			</view>
			<view class="nav-bar-title">
				会展详情
			</view>
			<view class="nav-bar-moreicon" @click="seemore()">
				<image src="../../static/moreIcon.png" mode=""></image>
			</view>
		</view>
		<view class="nav-bar-zw"></view>
		<view class="big-pic-area">
			<image src="https://img.js.design/assets/img/6401dee4a17d88f54fbab993.png#4e15ed8d4ae932d96f84ff97cc4ae1ee" alt="">
		</view>
		<view class="detail-title">
			深圳国际现代绿色农业博览会
		</view>
		<view class="detail-position">
			·地址：深圳会展中心
		</view>
		<view class="detail-time">
			·日期：12.30-1.1
		</view>
		<view class="detail-contact">
			·联系方式：深圳市绿然展业发展有限公司 0755-33358102
		</view>
		<view class="info-detail-num">
			·4种展位出租中
		</view>
		<view class="info-detail-zs-title">
			展商名录：
		</view>
		<scroll-view scroll-x="true" class="info-detail-zs-list">
			<view class="info-detail-zs-item" v-for="(item,index) in 10">
				<view class="info-detail-zs-item-imgarea">
					<image src="https://img.js.design/assets/img/64054f5eb4c3cf53d9720d1c.jpeg#687ed74a3007377a7b429127e97e3258" mode=""></image>
				</view>
				<view class="info-detail-zs-item-namearea">
					中达新材料
				</view>
			</view>	
		</scroll-view>
		<view class="info-detail-idiographic-title">
			展会详情：
		</view>
		<view class="info-detail-idiographic-description">
			深圳国际会展中心位于深圳市宝安区福永街道的会展新城片区，地处粤港澳大湾区湾顶、珠三角中心和广东自贸区中心，广深港核心发展走廊和东西向发展走廊的交会处，广佛肇、深莞惠和珠中江三大城市圈交会处  ，是深圳市委市政府布局深圳空港新城“两中心一馆”的三大主体建筑之一.
		</view>
		<view class="bottom-area-zw"></view>
		<view class="bottom-area">
			<view class="contact-zh" @click="contactZH()">
				<image src="../../static/contactzh.png" mode=""></image>
				<view class="contact-zh-title">
					联系展会
				</view>
			</view>
			<view class="join-zh" @click="joinZH()">
				<image src="../../static/joinzh.png" mode=""></image>
				<view class="join-zh-title">
					参加展会
				</view>
			</view>
			<view class="collect-zh" @click="collectZH()">
				<image src="../../static/collectzh.png" mode=""></image>
				<view class="collect-zh-title">
					收藏展会
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			goback(){
				uni.navigateBack({
					delta:1
				})
			},
			seemore(){
				uni.showToast({
					icon:"error",
					title:"功能暂未开通"
				})
			},
			contactZH(){
				uni.showToast({
					icon:"error",
					title:"功能暂未开通"
				})
			},
			joinZH(){
				uni.navigateTo({
					url:"../JoinZHPage/JoinZHPage"
				})
			},
			collectZH(){
				uni.showToast({
					icon:"error",
					title:"功能暂未开通"
				})
			}
		}
	}
</script>

<style>
	.content{
		background-color: #ebedf8;
		width: 100vw;
		/* height: 100vh; */
	}
	.status-bar{
		height: var(--status-bar-height);
		width: 100%;
		/* background-color: aquamarine; */
		position: fixed;
		z-index: 1000;
		background-color: #ebedf8;
	}
	.status-bar-zw{
		height: var(--status-bar-height);
		width: 100%;
	}
	.nav-bar{
		width: 100%;
		height: 100rpx;
		background-color: #ebedf8;
		/* background-color: aquamarine; */
		display: flex;
		align-items: center;
		justify-content: space-between;
		position: fixed;
		z-index: 999;
	}
	.nav-bar-backicon{
		height: 100rpx;
		width: 100rpx;
		/* background-color: black; */
	}
	.nav-bar-backicon image{
		/* width: 50%; */
		/* height: 50%; */
		width: 100%;
		height: 100%;
	}
	.nav-bar-title{
		height: 100rpx;
		/* background-color: aqua; */
		display: flex;
		align-items: center;
		justify-content: center;
		font-weight: 600;
		letter-spacing: 0.02em;
	}
	.nav-bar-moreicon{
		height: 100rpx;
		width: 100rpx;
		/* background-color: black; */
	}
	.nav-bar-moreicon image{
		/* width: 50%; */
		/* height: 50%; */
		width: 100%;
		height: 100%;
	}
	.nav-bar-zw{
		height: 100rpx;
		width: 100%;
	}
	.big-pic-area{
		width: 100%;
	}
	.big-pic-area image{
		width: 100%;
	}
	.detail-title{
		margin-top: 20rpx;
		font-size: 40rpx;
		margin-left: 40rpx;
		font-weight: 600;
		margin-right: 30rpx;
	}
	.detail-position{
		margin-left: 40rpx;
		margin-top: 20rpx;
		line-height: 50rpx;
		margin-right: 30rpx;
	}
	.detail-time{
		margin-left: 40rpx;
		margin-top: 5rpx;
		line-height: 50rpx;
		margin-right: 30rpx;
	}
	.detail-contact{
		margin-left: 40rpx;
		margin-top: 5rpx;
		margin-right: 30rpx;
		line-height: 50rpx;
	}
	.info-detail-zs-title{
		margin-bottom: 10rpx;
		margin-left: 40rpx;
		margin-top: 10rpx;
		margin-right: 30rpx;
		line-height: 50rpx;
		font-size: 40rpx;
		font-weight: 600;
	}
	.info-detail-zs-list{
		/* background-color: aquamarine; */
		width: 90vw;
		margin-left: 5vw;
		height: 10vh;
		white-space: nowrap;
	}
	.info-detail-zs-items{
		
	}
	.info-detail-zs-item{
		display: inline-block;
		/* background-color: bisque; */
		height: 10vh;
		width: 15vh;
		margin-right: 20rpx;
		text-align: center;
		margin-top: 0.5vh;
	}
	.info-detail-zs-item-imgarea{
		height: 6vh;
		width: 10vh;
		/* background-color: black; */
		margin-left: 2.5vh;
	}
	.info-detail-zs-item-imgarea image{
		width: 100%;
		height: 100%;
	}
	.info-detail-idiographic-title{
		margin-left: 40rpx;
		margin-top: 10rpx;
		margin-right: 30rpx;
		line-height: 50rpx;
		font-size: 40rpx;
		font-weight: 600;
	}
	.info-detail-idiographic-description{
		margin-left: 40rpx;
		margin-top: 5rpx;
		margin-right: 30rpx;
		line-height: 50rpx;
	}
	.info-detail-num{
		margin-left: 40rpx;
		margin-top: 5rpx;
		margin-right: 30rpx;
		line-height: 50rpx;
	}
	.bottom-area-zw{
		height: 6vh;
		width: 100%;
		/* background-color: aqua; */
	}
	.bottom-area{
		height:6vh;
		width: 100%;
		position: fixed;
		top: 94vh;
		background-color: aquamarine;
		display: flex;
		align-items: center;
		justify-content: space-between;
		background: rgba(133, 154, 242, 1);
	}
	.contact-zh{
		height: 6vh;
		width: 33.33vw;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.contact-zh image{
		height: 3vh;
		width: 3vh;
	}
	.join-zh{
		height: 6vh;
		width: 33.33vw;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.join-zh image{
		height: 3vh;
		width: 3vh;
	}
	.collect-zh{
		height: 6vh;
		width: 33.33vw;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.collect-zh image{
		height: 3vh;
		width: 3vh;
	}
</style>
