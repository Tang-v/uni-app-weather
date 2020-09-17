<template>
	<view class="index_full">
		<!-- 当前城市今日天气 -->
		<view class="index_1">
			<!-- 定位当前城市 -->
			<view class="index_1_add">
				<view class="index_1_add_city">{{city}}</view>
				<uni-icons type="location-filled" size="22"></uni-icons>
			</view>
			<!-- 当前温度详情 -->
			<view class="index_1_T">
				<!-- 当前温度 -->
				<view class="index_1_T_now">
					<text class="index_1_T_now_text01">{{temp}}</text>
					<text class="index_1_T_now_text02">℃</text>
				</view>
				<!-- 今日温度区间 -->
				<view class="index_1_T_day">
					<text>{{temphigh}}℃</text>
					/
					<text>{{templow}}℃</text>
				</view>
				<!-- 详情  如多云，空气质量 -->
				<view class="index_1_T_more">
					<view>{{weather}}</view>
					<view>空气指数:{{aqi.aqi}}</view>
				</view>
			</view>
		</view>
		<!-- 今日天气变化表 -->
		<view class="index_2">
			<view class="index2_big">
				<view class="index_2_view" v-for="item in arr.hourly" :key="item.time">
					<!-- 时间  整时温度 -->
					<view class="index_2_time">
						<text>{{item.time}}</text>
					</view>
					<!-- 太阳  多云  下雨  图标 -->
					<view class="index_2_icon">{{item.weather}}</view>
					<!-- 时间对应当前温度 -->
					<view class="index_2_timeT">
						<text>{{item.temp}}℃</text>
					</view>
				</view>
			</view>
		</view>
		<!-- 未来七天的天气 -->
		<view class="index_3">
			<view class="index_3_day" v-for="item in week_date" :key="item.time">
				<view class="index_3_date">{{item.date}}&nbsp;&nbsp;{{item.week}}</view>
				<view class="index_3_win">{{item.day.weather}}/{{item.day.winddirect}}</view>
				<view class="index_3_T">{{item.night.templow}}℃/{{item.day.temphigh}}℃</view>
			</view>
		</view>
		<view class="weather_zhe">
		 <mckou-weather :weatherData="weatherData" ref="mckouWeather"></mckou-weather>
		</view>
		<!-- 星座运势 -->
		<view class="index_4">
			<view class="index_4_left">
				星座运势
			</view>
			<view class="index_4_right" @click="goHoroscope">
				点击查看你感兴趣的星座运势
			</view>
		</view>
		<!-- 历史上的今天 -->
		<view class="index_5">
			<view class="index_5_title" @click="goHistory">查看<历史上的今天></view>
		</view>
		<!-- 底部 -->
		<view class="index_6">
			<view class="index_6_view">天气版本：1.0.0</view>
			<view class="index_6_view" @click="goStatement">关于天气与隐私的声明</view>
			<view class="index_6_view">版本所有：果子狸</view>
		</view>
	</view>
</template>

<script>
	import uniIcons from "@/components/uni-icons/uni-icons.vue"
	import mckouWeather from '../../mckou-weather/mckouWeather.vue'
	export default {
		components: {
			uniIcons,
			mckouWeather
		},
		data() {
			return {
				weather:'',
				city: '',
				temp: '',
				info: '',
				aqi: '',
				arr: '',
				time: '',
				week_date:'',
				temphigh:'',
				templow:'',
				winddirect:'',
				weatherData:[]
			}
		},
		onLoad() {
				this.timeWeather()
		},
		methods: {
			//跳转到星座运势页面
			goHoroscope: function(e) {
				uni.navigateTo({
					url: '../horoscope/horoscope'
				});
			},
			//跳转声明页面
			goStatement: function(e) {
				uni.navigateTo({
					url: '../statement/statement'
				});
			},
			//跳转到历史上的今天
			goHistory: function(e) {
				uni.navigateTo({
					url: '../history/history'
				});
			},
			//天气时刻接口
			timeWeather: function(e) {
				var that = this;
				console.log(e)
				uni.request({
					url: 'https://way.jd.com/jisuapi/weather',
					data: {
						appkey: '2710d50da1ec526060533e38bb7a25fd',
						city: '南宁'
					},
					success: (res) => {
						// console.log(res.data);
						//城市
						this.city = res.data.result.result.city;
						//此刻温度
						this.temp = res.data.result.result.temp;
						// 最高温度
						this.temphigh = res.data.result.result.temphigh;
						// 最低温度
						this.templow = res.data.result.result.templow;
						// 天气  如晴
						this.weather = res.data.result.result.weather;
						//空气指数
						this.aqi = res.data.result.result.aqi;
						this.arr = res.data.result.result
						this.week_date = res.data.result.result.daily
						this.weatherData = res.data.result.result.daily
						console.log(res.data.result.result.daily)
						for(let i in this.week_date){
							let month = this.week_date[i].date.substr(5, 2)
							let day = this.week_date[i].date.substr(8, 2)
							this.week_date[i].date = month + '/' + day 
						}
						that.$nextTick(() => {
						    that.$refs.mckouWeather.init();
						});
					}
				});
			}
		}
	}
</script>

<style>
	page {
		background: url(../../static/bg.jpg);
		background-size: 100% 100%;
	}

	.index_full {
		display: flex;
		flex-direction: column;
		justify-content: center;
	}

	/* 当前城市今日天气 */
	.index_1 {
		width: 700rpx;
		height: 500rpx;
		margin: 0 auto;
	}

	.index_1_add {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		height: 100rpx;
	}

	.index_1_add_city {
		margin: 0 10rpx;
		font-size: 32rpx;
	}

	.index_1_T_now {
		height: 180rpx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
	}

	.index_1_T_now_text01 {
		font-size: 150rpx;
	}

	.index_1_T_day {
		display: flex;
		flex-direction: row;
		justify-content: center;
		font-size: 30rpx;
		margin: 10rpx 0;
	}

	.index_1_T_more {
		display: flex;
		flex-direction: column;
		justify-content: center;
		font-size: 30rpx;
		text-align: center;
		margin: 15rpx 0;
	}

	/* 今日天气变化表 */
	.index_2 {
		overflow-x: scroll;
		display: flex;
		flex-direction: row;
		width: 100%;
		height: 200rpx;
		margin: 10rpx auto;
	}
	
	.index2_big{
		display: flex;
		flex-direction: row;
		justify-content: center;
		width: 1600px;
		text-align: center;
	}

	.index_2_view {
		width: 50px;

	}

	.index_2_icon {
		margin: 10rpx 0;
		font-size: 30rpx;
	}

	.index_2_time,
	.index_2_timeT text {
		font-size: 28rpx;
	}

	/* 未来五天的天气 */
	.index_3 {
		display: flex;
		flex-direction: column;
		justify-content: center;
		width: 700rpx;
		height: 400rpx;
		margin: 20rpx auto;
	}

	.index_3_day {
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		padding: 5rpx 0;
		font-size: 30rpx;
		margin: 20rpx 0;
	}

	.index_3_date {
		width: 220rpx;
		text-align: center;
	}

	.index_3_weather {
		width: 80rpx;
	}

	.index_3_weather_img {
		width: 50rpx;
		height: 50rpx;
	}
	
	.index_3_win{
		width: 280rpx;
		text-align: center;
	}

	/* 星座运势 */
	.index_4 {
		display: flex;
		flex-direction: row;
		align-items: center;
		width: 650rpx;
		height: 100rpx;
		margin: 20rpx auto;
		background: #ffffff73;
		border-radius: 15rpx;
		font-size: 30rpx;
	}

	.index_4_left {
		width: 250rpx;
		height: 50rpx;
		display: flex;
		align-items: center;
		justify-content: center;
		border-right: 1px solid #a1a1a1;
	}

	.index_4_right {
		width: 550rpx;
		height: 100rpx;
		display: flex;
		align-items: center;
		margin: 0 30rpx;
	}

	/* 博君一笑 */
	.index_5 {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		width: 500rpx;
		height: 100rpx;
		margin: 10rpx auto;
		background: #ffffff73;
		border-radius: 15rpx;
	}

	.index_5_title{
		font-size: 35rpx;
	}

	/* 底部 */
	.index_6 {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: 700rpx;
		height: 150rpx;
		margin: 10rpx auto;
		font-size: 25rpx;
	}

	.index_6_view {
		padding: 5rpx 0;
	}
</style>
