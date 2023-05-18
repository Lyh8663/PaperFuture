<template>
	<view class="content">
		<view class="status-bar"></view>
		<view class="status-bar-zw"></view>
		<view class="logo-area">
			<image src="../../static/pflogo.png" mode=""></image>
		</view>
		<view class="great-word-area">
			你好！
		</view>
		<view class="account-password-area">
			<view class="account-area">
				<view class="account-title">
					用户名：
				</view>
				<input type="text" class="account-input-area" placeholder="请输入账号" v-model="account">
			</view>
			<view class="password-area">
				<view class="account-title">
					密&nbsp;&nbsp;&nbsp;码：
				</view>
				<input type="password" class="account-input-area" placeholder="请输入密码" v-model="password">
			</view>
		</view>
		<view class="btn-area">
			<button @click="login()">登录</button>
			<button @click="regist()">注册</button>
		</view>
		<view class="other-way-title">
			- - - 其他登录方式 - - -
		</view>
		<view class="other-way-icons">
			<view class="icon-area" @click="qqlogin()">
				<image src="../../static/qqicon.png" mode=""></image>
			</view>
			<view class="icon-area" @click="wxlogin()">
				<image src="../../static/wxicon.png" mode=""></image>
			</view>
			<view class="icon-area" @click="tblogin()">
				<image src="../../static/tbicon.png" mode=""></image>
			</view>
			<view class="icon-area" @click="wblogin()">
				<image src="../../static/wbicon.png" mode=""></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				account:'',
				password:''
			}
		},
		methods: {
			login(){
				//登录成功判断
				if(this.account=='gzy666'&&this.password=='2023hlw+'){
					console.log("账号密码正确");
					uni.switchTab({
						url:"../index/index"
					})
				}else{
					console.log("账号密码失败");
					uni.showToast({
						icon:"error",
						title:"账号或密码错误"
					})
				}
			},
			regist(){
				uni.showToast({
					icon:"error",
					title:"功能暂未开通"
				})
			},
			qqlogin(){
				uni.showToast({
					icon:"error",
					title:"功能暂未开通"
				})
			},
			wxlogin(){
				uni.showToast({
					icon:"error",
					title:"功能暂未开通"
				})
			},
			tblogin(){
				uni.showToast({
					icon:"error",
					title:"功能暂未开通"
				})
			},
			wblogin(){
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
		height: 100vh;
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
	.logo-area{
		height: 12vh;
		width: 45vw;
		padding-top: 10vh;
		padding-left: 10vw;
	}
	.logo-area image{
		width: 100%;
		height: 100%;
	}
	.great-word-area{
		padding-top: 1vh;
		padding-left: 10vw;
		font-size: 70rpx;
	}
	.account-password-area{
		margin-top: 10vh;
		padding-left: 10vw;
		width: 80vw;
		padding-right: 10vw;
		/* background-color: aquamarine; */
	}
	.account-area{
		width: 100%;
		height: 7vh;
		display: flex;
		align-items: center;
	}
	.account-title{
		flex: 4;
		/* background-color: antiquewhite; */
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 40rpx;
	}
	.account-input-area{
		flex: 6;
		background-color: antiquewhite;
		display: flex;
		align-items: center;
		justify-content: center;
		text-align: center;
		background-color: aliceblue;
		font-size: 40rpx;
		height: 4vh;
		border-radius: 1000rpx;
		border: 1px solid grey;
		
	}
	.password-area{
		width: 100%;
		height: 7vh;
		display: flex;
		align-items: center;
	}
	.btn-area{
		width: 80vw;
		margin-left: 10vw;
		margin-right: 10vw;
		height: 6vh;
		margin-top: 3vh;
		/* background-color: aquamarine; */
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	.btn-area button{
		width: 30vw;
		height: 100%;
		background-color: rgba(133, 154, 242, 1);
		font-size: 28rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		color: white;
	}
	.other-way-title{
		margin-top: 15vh;
		width: 80vw;
		margin-left: 10vw;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.other-way-icons{
		width: 80vw;
		margin-left: 10vw;
		display: flex;
		align-items: center;
		justify-content: space-evenly;
	}
	.icon-area{
		height: 10vw;
		width: 10vw;
		margin-top: 2vh;
		/* background-color: black; */
	}
	.icon-area image{
		width: 100%;
		height: 100%;
	}
</style>
