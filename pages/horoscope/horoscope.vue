<template>
	<view class="start">
		<view class="start_f1">
			<view class="start_f1_01" @click="goHoroscopemore" data-name="白羊座">
				<image src="../../static/baiyang.png" class="start_img"></image>
				<view class="start_title">白羊座</view>
				<view class="start_date">3.21-4.19</view>
			</view>
			<view class="start_f1_01" @click="goHoroscopemore" data-name="金牛座">
				<image src="../../static/niu.png" class="start_img"></image>
				<view class="start_title">金牛座</view>
				<view class="start_date">4.20-5.20</view>
			</view>
			<view class="start_f1_01" @click="goHoroscopemore" data-name="双子座">
				<image src="../../static/shuang.png" class="start_img"></image>
				<view class="start_title">双子座</view>
				<view class="start_date">5.21-6.21</view>
			</view>
		</view>
		<view class="start_f1">
			<view class="start_f1_01" @click="goHoroscopemore" data-name="巨蟹座">
				<image src="../../static/juxie.png" class="start_img"></image>
				<view class="start_title">巨蟹座</view>
				<view class="start_date">6.22-7.22</view>
			</view>
			<view class="start_f1_01" @click="goHoroscopemore" data-name="狮子座">
				<image src="../../static/lion.png" class="start_img"></image>
				<view class="start_title">狮子座</view>
				<view class="start_date">7.23-8.22</view>
			</view>
			<view class="start_f1_01" @click="goHoroscopemore" data-name="处女座">
				<image src="../../static/chunv.png" class="start_img"></image>
				<view class="start_title">处女座</view>
				<view class="start_date">8.23-9.22</view>
			</view>
		</view>
		<view class="start_f1">
			<view class="start_f1_01" @click="goHoroscopemore" data-name="天秤座">
				<image src="../../static/tianchen.png" class="start_img"></image>
				<view class="start_title">天秤座</view>
				<view class="start_date">9.23-10.23</view>
			</view>
			<view class="start_f1_01" @click="goHoroscopemore" data-name="天蝎座">
				<image src="../../static/tianxie.png" class="start_img"></image>
				<view class="start_title">天蝎座</view>
				<view class="start_date">10.24-11.22</view>
			</view>
			<view class="start_f1_01" @click="goHoroscopemore" data-name="射手座">
				<image src="../../static/sheshou.png" class="start_img"></image>
				<view class="start_title">射手座</view>
				<view class="start_date">11.23-12.21</view>
			</view>
		</view>
		<view class="start_f1">
			<view class="start_f1_01" @click="goHoroscopemore" data-name="摩羯座">
				<image src="../../static/mojie.png" class="start_img"></image>
				<view class="start_title">摩羯座</view>
				<view class="start_date">12.22-1.19</view>
			</view>
			<view class="start_f1_01" @click="goHoroscopemore" data-name="水瓶座">
				<image src="../../static/shuip.png" class="start_img"></image>
				<view class="start_title">水瓶座</view>
				<view class="start_date">1.20-2.18</view>
			</view>
			<view class="start_f1_01" @click="goHoroscopemore" data-name="双鱼座">
				<image src="../../static/yu.png" class="start_img"></image>
				<view class="start_title">双鱼座</view>
				<view class="start_date">2.19-3.20</view>
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
			//跳转到星座详情页
			goHoroscopemore: function(e) {
				console.log(e.currentTarget.dataset.name)
				uni.navigateTo({
					url: '../horoscope_more/horoscope_more?movieName='+e.currentTarget.dataset.name
				});
			},
		}
	}
</script>

<style>
	page{
		background: #f1f9fc;
	}
	
	.start{
		display: flex;
		flex-direction: column;
		justify-content: center;
	}
	
	.start_f1{
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		width: 700rpx;
		height: 300rpx;
		margin: 0 auto;
	}
	
	.start_f1_01{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	
	.start_img{
		width: 90rpx;
		height: 90rpx;
	}
	
	.start_title{
		font-size: 33rpx;
		margin: 10rpx 0;
	}
	
	.start_date{
		font-size: 26rpx;
	}
</style>
