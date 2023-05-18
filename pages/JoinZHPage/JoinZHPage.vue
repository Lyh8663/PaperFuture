<template>
	<view class="content">
		<view class="status-bar"></view>
		<view class="status-bar-zw"></view>
		<view class="nav-bar">
			<view class="nav-bar-backicon" @click="goback()">
				<image src="../../static/backIcon.png" mode=""></image>
			</view>
			<view class="nav-bar-title">
				组织参展
			</view>
			<view class="nav-bar-moreicon" @click="seemore()">
				<image src="../../static/moreIcon.png" mode=""></image>
			</view>
		</view>
		<view class="nav-bar-zw"></view>
		<view class="nav-bar-position">
			<view class="nav-bar-position-title">
				当前：xx市xx展
			</view>
		</view>
		<view class="choose-shape-num">
			<view :class="['three-three',this.chosenindex==1?'itemChosen':'']" @click="changeIndex(1)">
				3*3规格
			</view>
			<view :class="['five-five',this.chosenindex==2?'itemChosen':'']" @click="changeIndex(2)">
				5*5规格
			</view>
			<view :class="['seven-seven',this.chosenindex==3?'itemChosen':'']" @click="changeIndex(3)">
				7*7规格
			</view>
		</view>
		<view class="num-underline-area">
			<view :class="['underline',this.chosenindex==1?'':'notChosen']">
				
			</view>
			<view :class="['underline',this.chosenindex==2?'':'notChosen']">
				
			</view>
			<view :class="['underline',this.chosenindex==3?'':'notChosen']">
				
			</view>
		</view>
		<view class="chooseArea">
			<view :class="['topwall',topwallchosen==1?'wallChosen':'']" @click="chooseTopWall()">
				
			</view>
			<view class="midArea1">
				<view :class="['leftwall',leftwallchosen==1?'wallChosen':'']" @click="chooseLeftWall()">
					
				</view>
				<view class="mid-items1" v-if="chosenindex==1">
					<view class="mid-item1" v-for="(item,number) in 9" @click="clickitem(number)">
						<!-- {{this.chosennums.indexOf(number)==-1?'':'已选'}} -->
						{{chosennums.indexOf(number)==-1?'':'已选'}}
					</view>
				</view>
				<view class="mid-items2" v-if="chosenindex==2">
					<view class="mid-item2" v-for="(item,number) in 25" @click="clickitem(number)">
						<!-- {{this.chosennums.indexOf(number)==-1?'':'已选'}} -->
						{{chosennums.indexOf(number)==-1?'':'已选'}}
					</view>
				</view>
				<view class="mid-items3" v-if="chosenindex==3">
					<view class="mid-item3" v-for="(item,number) in 49" @click="clickitem(number)">
						<!-- {{this.chosennums.indexOf(number)==-1?'':'已选'}} -->
						{{chosennums.indexOf(number)==-1?'':'已选'}}
					</view>
				</view>
				<view :class="['rightwall',rightwallchosen==1?'wallChosen':'']" @click="chooseRightWall()">
					
				</view>
			</view>
			<view :class="['bottomwall',bottomwallchosen==1?'wallChosen':'']" @click="chooseBottomWall()">
				
			</view>
			<view class="choose-title">
				请在上图选择您的展位样式(长矩形为墙板)
			</view>
			<view class="enter-scale-area">
				<view class="enter-scale-title">
					<view class="enter-scale-title-main">
						单位长度:
					</view>
					<view class="enter-scale-title-sub">
						小方格的边长
					</view>
				</view>
				<view class="enter-scale-input">
					<input type="text" placeholder="长度">
					<view class="enter-scale-input-m">
						m
					</view>
				</view>
				<view class="scale-op">
					*
				</view>
				<view class="enter-scale-input">
					<input type="text" placeholder="宽度">
					<view class="enter-scale-input-m">
						m
					</view>
				</view>
			</view>
			<view class="zh-2d-pic-title">
				展会平面图
			</view>
			<view class="zh-2d-pic">
				<image src="https://img.js.design/assets/img/6401e67a753ee73843709fc4.png#9e4f9ab2fc79483557d602c350a041b1" mode=""></image>
			</view>
			<view class="btn-area">
				<button @click="toZHShopPage()">确认</button>
			</view>
			<view class="warn-title">
				请确认是否与购买的展位一致
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				chosenindex:1,
				chosennums:[],
				topwallchosen:0,
				leftwallchosen:0,
				rightwallchosen:0,
				bottomwallchosen:0
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
			changeIndex(i){
				this.chosenindex = i;
				console.log(this.chosenindex + "chosen")
				//切换规格的时候，清空已选内容
				this.chosennums = [];
				this.leftwallchosen = 0;
				this.rightwallchosen = 0;
				this.topwallchosen = 0;
				this.bottomwallchosen = 0;
			},
			chooseTopWall(){
				if(this.topwallchosen==0){
					this.topwallchosen = 1;
				}else{
					this.topwallchosen = 0;
				}
			},
			chooseBottomWall(){
				if(this.bottomwallchosen==0){
					this.bottomwallchosen = 1;
				}else{
					this.bottomwallchosen = 0;
				}
			},
			chooseLeftWall(){
				if(this.leftwallchosen==0){
					this.leftwallchosen = 1;
				}else{
					this.leftwallchosen = 0;
				}
			},
			chooseRightWall(){
				if(this.rightwallchosen==0){
					this.rightwallchosen = 1;
				}else{
					this.rightwallchosen = 0;
				}
			},
			clickitem(i){
				console.log(i + "被点击");
				var existIndex = -1;
				for(var j = 0;j<this.chosennums.length;j++){
					if(this.chosennums[j]==i){//如果已经存在
						existIndex = j;
					}
				}
				if(existIndex == -1){
					this.chosennums.push(i);
				}
				if(existIndex != -1){
					this.chosennums.splice(existIndex, 1)
				}
				// console.log(this.chosennums);
				for(var s = 0;s<this.chosennums.length;s++){
					console.log("num:" + this.chosennums[s]);
				}
			},
			toZHShopPage(){
				uni.navigateTo({
					url:"../ZHShopPage/ZHShopPage"
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
		z-index: 999;
		background-color: #ebedf8;
	}
	.status-bar-zw{
		height: var(--status-bar-height);
		width: 100%;
	}
	.nav-bar{
		width: 100%;
		height: 100rpx;
		/* background-color: aquamarine; */
		display: flex;
		align-items: center;
		justify-content: space-between;
		position: fixed;
		background-color: #ebedf8;
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
	.nav-bar-position{
		height: 80rpx;
		width: 100%;
		/* background-color: aquamarine; */
		display: flex;
		align-items: center;
		/* font-weight: 600; */
		font-size: 35rpx;
	}
	.nav-bar-position-title{
		margin-left: 5vw;
	}
	.choose-shape-num{
		/* background-color: aquamarine; */
		height: 60rpx;
		margin-top: 5rpx;
		display: flex;
		align-items: center;
		justify-content: space-evenly;
	}
	.num-underline-area{
		display: flex;
		align-items: center;
		justify-content: space-evenly;
		width: 100%;
		height: 5rpx;
		width: 100%;
	}
	.underline{
		width: 19vw;
		height: 100%;
		background-color: grey;
	}
	.itemChosen{
		font-weight: 600;
	}
	.notChosen{
		/* display: none; */
		background-color: #ebedf8;
	}
	.topwall{
		border: 1px solid black;
		width: 80vw;
		height: 3vw;
		margin-left: 10vw;
		margin-bottom: 1vw;
		margin-top: 4vw;
	}
	.bottomwall{
		border: 1px solid black;
		width: 80vw;
		height: 3vw;
		margin-left: 10vw;
		margin-top: 1vw;
	}
	.midArea1{
		height: calc(80vw + 2px);
		width: calc(80vw + 6vw + 2vw + 2px);
		/* background-color: white; */
		margin-left: calc(6vw);
		display: flex;
	}
	.leftwall{
		height: 80vw;
		width: 3vw;
		border: 1px solid black;
		margin-right: 1vw;
	}
	.rightwall{
		height: 80vw;
		width: 3vw;
		border: 1px solid black;
		margin-left: 1vw;
	}
	.mid-items1{
		width: 80vw;
		height: 80vw;
		/* background-color: aliceblue; */
		display: flex;
		flex-wrap: wrap;
		/* justify-content: ; */
		/* background-color: white; */
	}
	.mid-item1{
		height: calc(78vw / 3);
		width: calc(78vw / 3);
		margin-left: 0.4vw;
		/* background-color: aqua; */
		background-color: white;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.mid-items2{
		width: 80vw;
		height: 80vw;
		/* background-color: aliceblue; */
		display: flex;
		flex-wrap: wrap;
		/* justify-content: ; */
		/* background-color: white; */
	}
	.mid-item2{
		height: calc(76vw / 5);
		width: calc(76vw / 5);
		margin-left: 0.5vw;
		/* background-color: aqua; */
		background-color: white;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.mid-items3{
		width: 80vw;
		height: 80vw;
		/* background-color: aliceblue; */
		display: flex;
		flex-wrap: wrap;
		/* justify-content: ; */
		/* background-color: white; */
	}
	.mid-item3{
		height: calc(75vw / 7);
		width: calc(75vw / 7);
		margin-left: 0.5vw;
		/* background-color: aqua; */
		background-color: white;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.wallChosen{
		background-color: rgba(164, 180, 243, 1);
	}
	.choose-title{
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-top: 3vw;
		margin-bottom: 3vw;
		color: gray;
	}
	.enter-scale-area{
		display: flex;
		width: 100%;
		/* background-color: aquamarine; */
		/* align-items: center; */
		justify-content: space-evenly;
	}
	.enter-scale-title{
		/* background-color: bisque; */
		width: 30vw;
	}
	.enter-scale-title-main{
		width: 100%;
		text-align: center;
	}
	.enter-scale-title-sub{
		width: 100%;
		text-align: center;
		font-size: 12px;
		color: gray;
	}
	.enter-scale-input{
		/* background-color: aqua; */
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.enter-scale-input input{
		width: 20vw;
		border: 1px solid black;
		height: 90%;
		border-radius: 1000rpx;
		margin-right: 10rpx;
		text-align: center;
		overflow: hidden;
	}
	.zh-2d-pic-title{
		margin-left: 5vw;
		margin-top: 5vw;
		font-weight: 600;
	}
	.zh-2d-pic{
		width: 90vw;
		margin-left: 5vw;
		margin-right: 5vw;
		margin-top: 3vw;
	}
	.zh-2d-pic image{
		width: 100%;
	}
	.btn-area{
		width: 100%;
		margin-bottom: 4vw;
		margin-top: 4vw;
		display: flex;
		justify-content: center
	}
	.btn-area button{
		width: 40vw;
		border-radius: 50rpx;
		background-color: rgba(133, 154, 242, 1);
		color: white;
	}
	.warn-title{
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: center;
		padding-bottom: 10vw;
		color: gray;
	}
</style>
