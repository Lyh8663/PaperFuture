<template>
	<view class="content">
		<view class="status-bar"></view>
		<view class="status-bar-zw"></view>
		<view class="nav-bar">
			<view class="nav-bar-backicon" @click="goback()">
				<image src="../../static/backIcon.png" mode=""></image>
			</view>
			<view class="nav-bar-title">
				布置展会
			</view>
			<view class="nav-bar-moreicon" @click="seemore()">
				<image src="../../static/moreIcon.png" mode=""></image>
			</view>
		</view>
		<view class="nav-bar-zw"></view>
		<view class="bgScreen">
			<!-- 阴影位置  -->
			<view style="padding: 0rpx;position: absolute;"
			:style="{top: mY+'rpx',left: (mX + 37.5) + 'rpx'}" v-show="hide">
				<!-- 阴影大小 -->
				<view style="background-color: rgba(0,0,0, 0.2);"
				:style="{width:(hideW) + 'rpx',height: (hideH) + 'rpx'}">	
				</view>
			</view>
			<!-- 生成的两个物体 -->
			<view v-for="(item,index) in data"
			class="create-item"
			style="
			padding: 0rpx;
			position: absolute;" 
			:style="{
				top:regions[item.regionID].y + 'rpx',
				left:regions[item.regionID].x+'rpx',
				width:(regions[item.regionID].wME) + 'rpx',
				height:(regions[item.regionID].hME) + 'rpx',
				}"
			@touchmove="move($event,item)"
			@touchstart="moveF(item)"
			@touchend="moveE(item.regionID)">
				<view style="background-color: white;width: 100%;height: 100%">
					<!-- <text>{{item.text}}</text> -->
					<image :src="item.pic" mode="" style="height: 100%;width: 100%;"></image>
				</view>
			</view>
		</view>
		<view class="btn-area">
			<view class="btn-two">
				<view :class="['self-choose',tc_index==1?'btn-chosen':'']" @click="selfChoose()">
					自选套餐
				</view>
				<view :class="['guding-choose',tc_index==2?'btn-chosen':'']" @click="gudingChoose()">
					固定套餐
				</view>
			</view>
			<view class="total-price">
				总价：{{totalPrice}}
			</view>
		</view>
		<view class="btn-area-zw">
			
		</view>
		<view class="good-list1" v-if="tc_index==1">
			<view class="good-list-left-area">
				<view :class="['desk',tp_index==1?'type-chosen':'']" @click="deskChoose()">
					桌
				</view>
				<view :class="['shelf',tp_index==2?'type-chosen':'']" @click="shelfChoose()">
					柜
				</view>
				<view :class="['chair',tp_index==3?'type-chosen':'']" @click="chairChoose()">
					椅
				</view>
				<view :class="['wall',tp_index==4?'type-chosen':'']" @click="wallChoose()">
					墙
				</view>
				<view :class="['other',tp_index==5?'type-chosen':'']" @click="otherChoose()">
					余
				</view>
			</view>
			<view class="good-list-right-area">
				<scroll-view scroll-y="true" class="good-card-area">
					<view class="good-card" v-for="(item,index) in deskList">
						<view class="good-card-pic">
							<image :src="item.pic" mode=""></image>
						</view>
						<view class="good-card-detail">
							<view class="good-detail-title">
								{{item.name}}
							</view>
							<view class="good-detail-material">
								材质：{{item.material}}
							</view>
							<view class="good-detail-size">
								尺寸：{{item.size}}
							</view>
							<view class="good-detail-carry">
								承重：{{item.carry}}
							</view>
							<view class="good-detail-priceAndNum">
								<view class="good-detail-price">
									{{item.price}}￥
								</view>
								<view class="good-choose-num">
									<view class="sub"  @click="subnum(item.num,index,item.type)">
										-
									</view>
									<view class="num">
										{{item.num}}
									</view>
									<view class="add" @click="addnum(item.num,index,item.type)">
										+
									</view>
								</view>
							</view>
						</view>
					</view>
				</scroll-view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				totalPrice:0,
				tc_index: 1,
				tp_index:1,
				chosenIMG:'https://img.js.design/assets/img/6401f76fb4c3cf53d9f65649.webp#2fd5a6be857ca8dca576ad279901a2a9',
				deskList:[
					{
						id:1,
						pic:'https://img.js.design/assets/img/6401f9dca13be61babcdf74f.png#c23e714ce26374394dc6e5f13b0598a9',
						name:'瓦楞纸双层桌',
						type:'桌',
						price:110,
						num:0,
						material:'轻质瓦楞纸',
						size:'500*1800*250',
						carry:'100kg'
					},
					{
						id:2,
						pic:'https://img.js.design/assets/img/6401f9981c76707ff37271cb.png#c663d608a74859715c486ebc954e31f0',
						name:'瓦楞纸书桌',
						type:'桌',
						price:99,
						num:0,
						material:'轻质瓦楞纸',
						size:'500*1800*250',
						carry:'100kg'
					},
					{
						id:3,
						pic:'https://img.js.design/assets/img/6401f9d0753ee73843743dbf.jpeg#f687c8fdfe3f2ae5e93254054e168809)',
						name:'瓦楞纸茶几',
						type:'桌',
						price:120,
						num:0,
						material:'轻质瓦楞纸',
						size:'500*1800*250',
						carry:'100kg'
					},
					{
						id:4,
						pic:'https://img.js.design/assets/img/6401f9dca13be61babcdf74f.png#c23e714ce26374394dc6e5f13b0598a9',
						name:'瓦楞纸双层桌',
						type:'桌',
						price:110,
						num:0,
						material:'轻质瓦楞纸',
						size:'500*1800*250',
						carry:'100kg'
					},
					{
						id:5,
						pic:'https://img.js.design/assets/img/6401f9981c76707ff37271cb.png#c663d608a74859715c486ebc954e31f0',
						name:'瓦楞纸书桌',
						type:'桌',
						price:99,
						num:0,
						material:'轻质瓦楞纸',
						size:'500*1800*250',
						carry:'100kg'
					},
					{
						id:6,
						pic:'https://img.js.design/assets/img/6401f9d0753ee73843743dbf.jpeg#f687c8fdfe3f2ae5e93254054e168809)',
						name:'瓦楞纸茶几',
						type:'桌',
						price:120,
						num:0,
						material:'轻质瓦楞纸',
						size:'500*1800*250',
						carry:'100kg'
					}
				],
				data:[],
				//两个方块后续位置
				regions:[],
				//阴影位置
				mY:0,
				mX:0,
				// 屏幕的宽高
				widthV:'',
				heightV:'',
				hide: false,
				hideW:0,
				hideH:0,
				//手机导航栏高度
				statusBarHeight: uni.getSystemInfoSync ().statusBarHeight
			}
		},
		methods: {
			move(e,item){
				// 判断当前移动到的区域是否有物品
				// this.isGoods(item.regionID)
				// 获取当前物体宽高
				let w = item.wME
				let h = item.hME
				// 获取当前位置(左上角的点)
				let newY = e.changedTouches[0].pageY*2 - h/2;
				let newX = e.changedTouches[0].pageX*2 - w/2;
				// console.log(e.changedTouches[0])
				//输出看一看这个$event内容是什么
				item.x = newX
				item.y = newY
				
				// 更新当前固定坐标的位置
				this.mY = Math.round(newY/h) * h;
				this.mX = Math.round(newX/w) * w ;//对准阴影
				this.regions[item.regionID] = item
				
				// 更新当前布局样式（产生拖动效果）
				this.$forceUpdate()
			},
			moveF(item){
				// 第一次点击物品时生成固定坐标位置，设置my和mx
				this.mY = this.regions[item.regionID].y
				this.mX = this.regions[item.regionID].x
				this.hide = true;//是阴影部分可见
				this.hideW = item.wME
				this.hideH = item.hME
			},
			moveE(id){
				this.hide = false
				// 固定当前位置
				let item = this.regions[id]
				// 获取当前物体宽高
				let w = item.wME
				let h = item.hME
				item.y = Math.round(item.y/h) * h
				item.x = Math.round(item.x/w) * w + 37.5
				
				// 判断当前是否超出边界
				// if(item.x < 37.5) item.x = 37.5;//可以弹回
				// if(item.x+w > this.widthV) item.x =Math.floor((this.widthV-w)/w)*w;
				// if(item.y < 0) item.y =0;
				
				// 修改位置信息
				this.regions[id] = item
				
				// 更新
				this.$forceUpdate()
			},
			selfChoose(){
				this.tc_index = 1;
				console.log(this.tc_index + "chosen")
			},
			gudingChoose(){
				this.tc_index = 2;
				console.log(this.tc_index + "chosen")
			},
			deskChoose(){
				this.tp_index = 1;
				console.log(this.tp_index + "chosen")
			},
			shelfChoose(){
				this.tp_index = 2;
				console.log(this.tp_index + "chosen")
			},
			chairChoose(){
				this.tp_index = 3;
				console.log(this.tp_index + "chosen")
			},
			wallChoose(){
				this.tp_index = 4;
				console.log(this.tp_index + "chosen")
			},
			otherChoose(){
				this.tp_index = 5;
				console.log(this.tp_index + "chosen")
			},
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
			addnum(a,b,c){
				console.log("增加前，数量num：" + a);
				console.log("操作数组：" + c);
				console.log("操作数组index：" + b);
				if(c=="桌"){
					this.deskList[b].num++;//数量增加
					this.totalPrice += this.deskList[b].price;//总价增加
				}
				console.log("增加后，数量num：" + this.deskList[b].num);
				//点击加号，需要让按钮出现在上方
				var temp_data={
					pic:'',
					regionID:'',
					wME:75,
					hME:75,
					type:'',
					id:''
				}
				var data_length = this.regions.length;//获取regions列表长度
				if(c=="桌"){
					temp_data.regionID = data_length;//设置region
					temp_data.pic = this.deskList[b].pic;//设置pic
					temp_data.type = c;//设置type
					temp_data.id = this.deskList[b].id//设置id
				}
				//将data列表进行扩容，现在可以显示三个物体
				this.data.push(temp_data);
				console.log(temp_data);
				console.log(this.data.length);
				//还需要将regions列表进行扩容
				var region_temp = {
					y:0,
					x:337.5,
					wME:75,
					wME:75,
					type:'',
					id:''
				}
				var regions_length = this.regions.length;
				if(c=="桌"){
					region_temp.y = 300;
					region_temp.type = c;//设置type
					region_temp.id = this.deskList[b].id;//设置id
				}
				//将regions列表进行扩容
				this.regions.push(region_temp);
				console.log(region_temp);
				console.log(this.regions.length);
				uni.showToast({
					icon:"success",
					title:"可以开摆了"
				})
			},
			subnum(a,b,c){
				console.log("减少前，数量num：" + a);
				console.log("操作数组：" + c);
				console.log("操作数组index：" + b);
				if(c=="桌"){
					if(this.deskList[b].num==0){
						uni.showToast({
							icon:"error",
							title:"数量已经为0"
						})
						return;
					}else{//不但减少数量，还需减少贴图
						//这样子删除是有bug的
						for(var i = 0;i<this.data.length;i++){
							if(this.data[i].type==c&&this.data[i].id==this.deskList[b].id){
								//此时应该删除data列表中的数据以及regions列表中的数据
								// this.regions.splice(i,1);
								this.data.splice(i, 1);
								var that = this;
								uni.showToast({
									icon:"success",
									title:"已删除目标",
									success() {
										that.deskList[b].num--;
										that.totalPrice -= that.deskList[b].price;//总价增加
										console.log("减少后，数量num：" + this.deskList[b].num);
									}
								})
								return;
							}
						}
					}
				}
				
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
	.bgScreen{
		/* background-color: aquamarine; */
		background-color: bisque;
		width: 90vw;
		height: 90vw;
		margin-left: 5vw;
		border-radius: 20rpx;
		overflow: hidden;
	}
	.create-item{
		z-index: 998;
		border-radius: 20rpx;
		overflow: hidden;
	}
	.big-pic-area image{
		/* margin-left: 5vw; */
		/* width: 90vw; */
		width: 100%;
		height: 100%;
		/* border-radius: 20rpx; */
	}
	.btn-area{
		display: flex;
		height: 5vh;
		width: 90vw;
		margin-left: 5vw;
		/* background-color: aquamarine; */
		padding-top: 0.5vh;
		align-items: center;
		padding-bottom: 1vh;
		/* justify-content: space-between; */
		/* position: fixed; */
		z-index: 998;
		background-color: #ebedf8;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	.btn-area-zw{
		width: 100%;
		/* height: 6.5vh; */
	}
	.btn-two{
		display: flex;
	}
	.total-price{
		color: brown;
		font-weight: 600;
	}
	.self-choose{
		/* background-color: bisque; */
		width: 25vw;
		color: rgba(53, 58, 85, 1);
		height: 4vh;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 20rpx;
		margin-right: 2vw;
	}
	.guding-choose{
		/* background-color: #fff; */
		width: 25vw;
		color: rgba(53, 58, 85, 1);
		height: 4vh;
		display: flex;
		align-items: center;
		justify-content: center;
		/* background-color: aquamarine; */
		border-radius: 20rpx;
	}
	.btn-chosen{
		background-color: rgba(53, 58, 85, 1);
		color: white;
		font-size: 26rpx;
	}
	.good-list1{
		width: 90vw;
		margin-left: 5vw;
		display: flex;
		/* margin-top: 1vh; */
		background-color: white;
		border-radius: 20rpx;
		overflow: hidden;
	}
	.good-list-left-area{
		width: 10vw;
		/* background-color: aquamarine; */
		height: 50vw;
		display: flex;
		flex-direction: column;
		align-items: center;
		font-size: 2vw;
		justify-content: space-evenly;
	}
	.desk{
		/* background-color: aqua; */
		width: 7vw;
		height: 7vw;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 10rpx;
	}
	.chair{
		/* background-color: aqua; */
		width: 7vw;
		height: 7vw;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 10rpx;
	}
	.shelf{
		/* background-color: aqua; */
		width: 7vw;
		height: 7vw;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 10rpx;
	}
	.wall{
		/* background-color: aqua; */
		width: 7vw;
		height: 7vw;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 10rpx;
	}
	.other{
		/* background-color: aqua; */
		width: 7vw;
		height: 7vw;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 10rpx;
	}
	.type-chosen{
		background-color: rgba(53, 58, 85, 1);
		color: white;
	}
	.good-list-right-area{
		/* background-color: aquamarine; */
		width: 80vw;
	}
	.good-card-area{
		height: 40vh;
		height: calc(100vh - 13.333333vw - 90vw - 6.5vh - 30px);
	}
	.good-card{
		width: 80vw;
		background-color: white;
		height: 30vw;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	.good-card-pic{
		width: 35vw;
		height: 90%;
		/* background-color: bisque; */
		border-radius: 10rpx;
		overflow: hidden;
	}
	.good-card-pic image{
		width: 100%;
		height: 100%;
	}
	.good-card-detail{
		width: 41vw;
		margin-left: 2vw;
		margin-right: 2vw;
		height: 90%;
	}
	.good-detail-title{
		font-size: 4vw;
		font-weight: 600;
	}
	.good-detail-material{
		font-size: 2vw;
	}
	.good-detail-size{
		font-size: 2vw;
	}
	.good-detail-carry{
		font-size: 2vw;
	}
	.good-detail-price{
		width: 15vw;
		color: red;
		font-weight: 600;
	}
	.good-detail-priceAndNum{
		/* background-color: aquamarine; */
		display: flex;
		align-items: center;
		justify-content: space-between;
		height: 9vw;
	}
	.good-choose-num{
		display: flex;
		/* background-color: bisque; */
		width: 26vw;
		align-items: center;
		justify-content: flex-end;
	}
	.sub{
		width: 4vw;
		height: 4vw;
		background-color: brown;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
	}
	.add{
		width: 4vw;
		height: 4vw;
		background-color: brown;
		display: flex;
		justify-content: center;
		align-items: center;
		color: white;
	}
	.num{
		background-color: white;
		width: 12vw;
		display: flex;
		align-items: center;
		justify-content: center;
	}
</style>
