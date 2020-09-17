<template>
	<view>
		<view class="history_title">{{year}}年{{month}}月{{day}}日</view>
		<view class="history_div" v-for="item in historyDate">
			<view class="history_div_title">
				<span>{{item.title}}</span>
			</view>
			<view class="history_div_date">
				<span>{{item.year}}年{{item.month}}月{{item.day}}日</span>
				<span>{{item.lunar}}</span>
			</view>
			<view class="history_div_text">
				<view v-if="item.pic==''"></view>
				<view v-else>
					<image :src="item.pic" class="history_div_src"></image>
				</view>
				<view class="history_div_des">{{item.des}}</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				historyDate:[],
				year:new Date().getFullYear(),
				month:new Date().getMonth()+1,
				day:new Date().getDate()
			}
		},
		//页面加载
		onLoad() {
			this.history()
		},
		methods: {
			//历史接口
			history: function() {
				uni.request({
					url: 'http://api.juheapi.com/japi/toh?key=69cbdf9cd9a97ac6bcd36ae8c2fb969e&v=1.0&month='+this.month+'&day='+this.day,
					success: (res) => {
						console.log(res.data.result);
						this.historyDate = res.data.result
					}
				});
			}
		}
	}
</script>

<style>
.history_title{
	width: 100%;
	height: 50rpx;
	text-align: center;
	font-size: 40rpx;
	margin: 10rpx 0;
}

.history_div{
	width: 700rpx;
	margin: 20rpx auto;
	border: 1px solid #eee;
	border-radius: 20rpx;
}

.history_div_date{
	display: flex;
	flex-direction: row;
	align-items: center;
}

.history_div_date span{
	margin-left: 20rpx;
	font-size: 30rpx;
	font-weight: bold;
}

.history_div_title{
	display: flex;
	flex-direction: row;
	align-items: center;
	justify-content: space-around;
	font-size: 40rpx;
	margin: 15rpx 0;
	font-weight: bold;
}

.history_div_text{
	display: flex;
	flex-direction: row;
	justify-content: center;
	align-items: center;
	margin: 20rpx;
}

.history_div_src{
	width: 200rpx;
	height: 200rpx;
	margin: 20rpx;
}

.history_div_des{
	font-size: 28rpx;
}
</style>
