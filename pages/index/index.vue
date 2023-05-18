<template>
	<view class="content">
		<view class="status-bar"></view>
		<view class="status-bar-zw"></view>
		<view class="nav-bar1">
			<view class="position-area">
				<view class="position-icon">
					<image src="../../static/positonIcon.png" mode=""></image>
				</view>
				<pickerAddress @change="change">
					<div class="city-name">{{txt}}</div>
				</pickerAddress>
			</view>
			<view class="take-photo-area">
				<image src="../../static/camera.png" mode=""></image>
			</view>
		</view>
		<view class="nav-bar1-zw"></view>
		<view class="nav-bar2">
			<view :class="['hz-info-title',chosenindex==1?'itemChosen':'']" @click="indexchoose(1)">
				会展信息
			</view>
			<view :class="['hz-mana-title',chosenindex==2?'itemChosen':'']" @click="indexchoose(2)">
				会展布置
			</view>
			<view :class="['wl-shop-title',chosenindex==3?'itemChosen':'']" @click="indexchoose(3)">
				瓦楞商城
			</view>
		</view>
		<view class="nav-bar2-zw"></view>
		<view class="nav-bar2-underline">
			<view :class="['hz-info-title-underline',chosenindex==1?'':'itemUnderlineNoChosen']">
			</view>
			<view :class="['hz-mana-title-underline',chosenindex==2?'':'itemUnderlineNoChosen']">
			</view>
			<view :class="['wl-shop-title-underline',chosenindex==3?'':'itemUnderlineNoChosen']">
			</view>
		</view>
		<view class="nav-bar2-underline-zw"></view>
		<view class="info-display-card" @click="toDetailPage()" v-for="(item, index) in 10" v-if="chosenindex==1">
			<view class="info-card">
				<view class="info-pic">
					<image src="https://img.js.design/assets/img/6401dee4a17d88f54fbab993.png#4e15ed8d4ae932d96f84ff97cc4ae1ee" mode=""></image>
				</view>
				<view class="info-detail">
					<view class="info-detail-title">
						第18届亚洲打印技术...
					</view>
					<view class="info-detail-position">
						地点：深圳会展中心
					</view>
					<view class="info-detail-time">
						日期：12.30-1.1
					</view>
					<view class="info-detail-checkdetail">
						查看详情 >
					</view>
				</view>
			</view>
		</view>
		<view class="bottom-area" v-if="chosenindex==1">
			- - - 上拉刷新 - - -
		</view>
	</view>
</template>

<script>
	import pickerAddress from '@/components/wangding-pickerAddress/wangding-pickerAddress.vue'
	export default {
		components:{
		    pickerAddress
		},
		data() {
			return {
				title: 'Hello',
				txt: '选择地址',
				//选项
				chosenindex:1
			}
		},
		computed:{
			
		},
		onLoad() {

		},
		methods: {
			change(data) {
			    this.txt = data.data.join('')
			    console.log(data.data.join(''))
			},
			indexchoose(i){
				this.chosenindex = i;
				console.log(i + "chosen")
			},
			toDetailPage(){
				console.log("跳转")
				uni.navigateTo({
					url:"../HZDetailPage/HZDetailPage"
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
		background-color: #ebedf8;
		z-index: 1000;
	}
	.status-bar-zw{
		height: var(--status-bar-height);
		width: 100%;
	}
	.nav-bar1{
		/* background-color: aqua; */
		width: 100%;
		height: 100rpx;
		display: flex;
		align-items: center;
		justify-content: space-between;
		position: fixed;
		z-index: 100;
		background-color: #ebedf8;
	}
	.nav-bar1-zw{
		height: 100rpx;
	}
	.position-area{
		/* background-color: aquamarine; */
		height: 100rpx;
		width: 60vw;
		display: flex;
		align-items: center;
		/* justify-content: space-between; */
	}
	.position-icon{
		height: 100rpx;
		width: 100rpx;
	}
	.position-icon image{
		height: 50%;
		width: 50%;
	}
	.position-icon {
		display: flex;
		align-items: center;
		justify-content: center;
		/* font-size: 40rpx; */
	}
	.city-name{
		font-size: 30rpx;
	}
	.take-photo-area{
		width: 100rpx;
		height: 100rpx;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.take-photo-area image{
		width: 50%;
		height: 50%;
	}
	.nav-bar2{
		/* background-color: aqua; */
		height: 60rpx;
		display: flex;
		align-items: center;
		justify-content: space-between;
		z-index: 99;
		background-color: #ebedf8;
		position: fixed;
		width: 100%;
	}
	.nav-bar2-zw{
		height: 60rpx;
	}
	.hz-info-title{
		margin-left: 10vw;
	}
	.wl-shop-title{
		margin-right: 10vw;
	}
	.nav-bar2-underline{
		height: 6rpx;
		width: 100%;
		/* background-color: aquamarine; */
		display: flex;
		align-items: center;
		justify-content: space-between;
		position: fixed;
		background-color: #ebedf8;
	}
	.nav-bar2-underline-zw{
		height: 6rpx;
	}
	/* background: rgba(122, 122, 122, 1); */
	.hz-info-title-underline{
		background: rgba(122, 122, 122, 1);
		width: 120rpx;
		height: 6rpx;
		border-radius: 10000000rpx;
		margin-left: 10vw;
	}
	.hz-mana-title-underline{
		background: rgba(122, 122, 122, 1);
		width: 120rpx;
		height: 6rpx;
		border-radius: 10000000rpx;
	}
	.wl-shop-title-underline{
		background: rgba(122, 122, 122, 1);
		width: 120rpx;
		height: 6rpx;
		border-radius: 10000000rpx;
		margin-right: 10vw;
	}
	.itemChosen{
		font-weight: 800;
	}
	.itemUnderlineNoChosen{
		background-color: #ebedf8;
	}
	.info-display-card{
		/* height: 50vh; */
		width: 90vw;
		/* background-color: antiquewhite; */
		background-color: white;
		margin-top: 20rpx;
		margin-left: 5vw;
		border-radius: 20rpx;
	}
	.info-zw-space{
		height: 2.5vw;
	}
	.info-card{
		height: 200rpx;
		width: 85vw;
		display: flex;
		align-items: center;
		justify-content: space-between;
		/* background-color: aqua; */
		margin-left: 2.5vw;
		/* margin-top: 20rpx; */
		/* margin-bottom: 20rpx; */
		padding-top: 2.5vw;
		padding-bottom: 2.5vw;
	}
	.info-pic{
		height: 200rpx;
		width: 35vw;
		/* background-color: aquamarine; */
		border-radius: 20rpx;
		overflow: hidden;
	}
	.info-pic image{
		width: 100%;
		height: 100%;
	}
	.info-detail{
		height: 200rpx;
		width: 48vw;
		/* background-color: bisque; */
	}
	.info-detail-title{
		/* font-size: 35rpx; */
		font-weight: 600;
	}
	.info-detail-position{
		color: gray;
		font-size: 26rpx;
		margin-top: 10rpx;
	}
	.info-detail-time{
		color: gray;
		font-size: 26rpx;
		margin-top: 10rpx;
	}
	.info-detail-checkdetail{
		height: 70rpx;
		width: 48vw;
		/* background-color: aqua; */
		display: flex;
		/* align-items: center; */
		align-items: flex-end;
		flex-direction: row-reverse;
		/* justify-content: end; */
		color: gray;
		font-size: 26rpx;
	}
	.bottom-area{
		height: 7vh;
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		letter-spacing: 0.1em;
	}
</style>
