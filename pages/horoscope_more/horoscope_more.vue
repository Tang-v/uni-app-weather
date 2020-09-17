<template>
	<view class="more">
		<view class="more_h"></view>
		<view class="more_head">
			<view class="more_head_title">
				<view v-if="todayName=='白羊座'" class="more_if">
					<image src="../../static/baiyang.png" class="more_head_img"></image>
					<text class="more_head_date">3.21-4.19</text>
				</view>
				<view v-if="todayName=='金牛座'" class="more_if">
					<image src="../../static/niu.png" class="more_head_img"></image>
					<text class="more_head_date">4.20-5.20</text>
				</view>
				<view v-if="todayName=='双子座'" class="more_if">
					<image src="../../static/shuang.png" class="more_head_img"></image>
					<text class="more_head_date">5.21-6.21</text>
				</view>
				<view v-if="todayName=='巨蟹座'" class="more_if">
					<image src="../../static/juxie.png" class="more_head_img"></image>
					<text class="more_head_date">6.22-7.22</text>
				</view>
				<view v-if="todayName=='狮子座'" class="more_if">
					<image src="../../static/lion.png" class="more_head_img"></image>
					<text class="more_head_date">7.23-8.22</text>
				</view>
				<view v-if="todayName=='处女座'" class="more_if">
					<image src="../../static/chunv.png" class="more_head_img"></image>
					<text class="more_head_date">8.23-9.22</text>
				</view>
				<view v-if="todayName=='天秤座'" class="more_if">
					<image src="../../static/tianchen.png" class="more_head_img"></image>
					<text class="more_head_date">9.23-10.23</text>
				</view>
				<view v-if="todayName=='天蝎座'" class="more_if">
					<image src="../../static/tianxie.png" class="more_head_img"></image>
					<text class="more_head_date">10.24-11.22</text>
				</view>
				<view v-if="todayName=='射手座'" class="more_if">
					<image src="../../static/sheshou.png" class="more_head_img"></image>
					<text class="more_head_date">11.23-12.21</text>
				</view>
				<view v-if="todayName=='摩羯座'" class="more_if">
					<image src="../../static/mojie.png" class="more_head_img"></image>
					<text class="more_head_date">12.22-1.19</text>
				</view>
				<view v-if="todayName=='水瓶座'" class="more_if">
					<image src="../../static/shuip.png" class="more_head_img"></image>
					<text class="more_head_date">1.20-2.18</text>
				</view>
				<view v-if="todayName=='双鱼座'" class="more_if">
					<image src="../../static/yu.png" class="more_head_img"></image>
					<text class="more_head_date">2.19-3.20</text>
				</view>
				<text class="more_head_name">{{todayName}}</text>
				<text class="more_head_today">{{today}}</text>
			</view>
			<view class="more_xing">
				<view class="more_heng">
					<view class="more_xing_f1">
						<view class="more_xing_f1_left">整体运势</view>
						<view class="more_xing_f1_right">{{todayall}}分</view>
					</view>
					<view class="more_xing_f1">
						<view class="more_xing_f1_left">爱情运势</view>
						<view class="more_xing_f1_right">{{todayLove}}分</view>
					</view>
				</view>
				<view class="more_heng">
					<view class="more_xing_f1">
						<view class="more_xing_f1_left">健康指数</view>
						<view class="more_xing_f1_right">{{todayHealth}}分</view>
					</view>
					<view class="more_xing_f1">
						<view class="more_xing_f1_left">财运运势</view>
						<view class="more_xing_f1_right">{{todayMoney}}分</view>
					</view>
				</view>
			</view>
			<view class="more_down">
				<view class="more_down_lucky">
					<view class="more_down_lucky_name">幸运数字</view>
					<view class="more_down_lucky_down">{{number}}</view>
				</view>
				<view class="more_down_lucky">
					<view class="more_down_lucky_name">幸运颜色</view>
					<view class="more_down_lucky_down">{{color}}</view>
				</view>
				<view class="more_down_lucky">
					<view class="more_down_lucky_name">速配星座</view>
					<view class="more_down_lucky_down">{{QFriend}}</view>
				</view>
			</view>
		</view>
		<view class="more_body">
			<template>
				<view>
					<uni-segmented-control :current="current" :values="items" @clickItem="onClickItem" style-type="button"></uni-segmented-control>
					<view class="content">
						<view v-if="current === 0" class="current_font">{{todaySummary}}</view>
						<view v-if="current === 1" class="current_font font_2">
							<view class="current_font_2">{{weekJob}}</view>
							<view class="current_font_2">{{weekLove}}</view>
							<view class="current_font_2">{{weekMoney}}</view>
							<view class="current_font_2">{{weekWork}}</view>
						</view>
						<view v-if="current === 2" class="current_font">{{monthAll}}</view>
						<view v-if="current === 3" class="current_font font_2">
							<view class="current_font_2">{{yeasCareer}}</view>
							<view class="current_font_2">{{yeasFinance}}</view>
							<view class="current_font_2">{{yeasHealth}}</view>
							<view class="current_font_2">{{yeasLove}}</view>
						</view>
					</view>
				</view>
			</template>
		</view>
	</view>
</template>

<script>
import uniSegmentedControl from '@/components/uni-segmented-control/uni-segmented-control.vue';
export default {
	components: { uniSegmentedControl },
	data() {
		return {
			items: ['今日概述', '本周运势', '本月运势', '本年运势'],
			current: 0,
			today:'',
			todayName:'',
			todayall:'',
			todayLove:'',
			todayHealth:'',
			todayMoney:'',
			number:'',
			color:'',
			QFriend:'',
			todaySummary:''
		};
	},
	//页面加载
	onLoad(e) {
		// console.log(e.movieName)
		let movieName = e.movieName
		this.horoscope(movieName)
	},
	methods: {
		//切换卡
		onClickItem(e) {
			if (this.current !== e.currentIndex) {
				this.current = e.currentIndex;
			}
		},
		//星座接口
		horoscope: function(e) {
			uni.request({
				url: 'http://web.juhe.cn:8080/constellation/getAll?key=c12e89f200ee20ba6d980dd1cb06ad14&consName='+e,
				success: (res) => {
					// console.log(res.data);
					// this.today = res.data.today.datetime
					this.todayName = res.data.today.name
					// //指数
					this.todayall = res.data.today.all
					this.todayLove = res.data.today.love
					this.todayHealth = res.data.today.health
					this.todayMoney = res.data.today.money
					// //幸运数
					this.QFriend = res.data.today.QFriend
					this.color = res.data.today.color
					this.number = res.data.today.number
					// //切换卡内容
					this.todaySummary = res.data.today.summary
					this.monthAll = res.data.month.all
					this.weekJob = res.data.week.job
					this.weekLove = res.data.week.love
					this.weekMoney = res.data.week.money
					this.weekWork = res.data.week.work
					this.yeasCareer = res.data.year.career
					this.yeasFinance = res.data.year.finance
					this.yeasHealth = res.data.year.health
					this.yeasLove = res.data.year.love
				}
			});
		}
	}
};
</script>

<style>
page {
	background: #b2e6ff;
}

.more {
	display: flex;
	flex-direction: column;
	justify-content: center;
}

.more_h {
	width: 100%;
	height: 100rpx;
}

.more_head {
	background: #fff;
	border-radius: 20rpx;
	width: 600rpx;
	height: 650rpx;
	margin: 0 auto;
	display: flex;
	flex-direction: column;
	justify-content: center;
}

.more_head_title {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	height: 250rpx;
}

.more_if{
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}

.more_head_img {
	width: 120rpx;
	height: 120rpx;
}

.more_head_date {
	font-size: 25rpx;
	color: #808080;
	margin: 10rpx 0;
}

.more_head_today{
	font-size: 28rpx;
}

.more_xing {
	display: flex;
	flex-direction: column;
	align-items: center;
	margin: 30rpx 0;
}

.more_heng{
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	align-items: center;
	margin: 10rpx 0;
}

.more_xing_f1 {
	font-size: 30rpx;
	margin: 10rpx 0;
	display: flex;
	flex-direction: row;
}

.more_xing_f1_left {
	width: 180rpx;
	text-align: center;
}

.more_xing_f1_right {
	width: 100rpx;
}

.more_down {
	display: flex;
	flex-direction: row;
	justify-content: space-around;
	align-items: center;
	margin-bottom: 20rpx;
}

.more_down_lucky {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}

.more_down_lucky_name {
	color: #999999;
	font-size: 25rpx;
	margin: 10rpx 0;
}

.more_down_lucky_down {
	margin: 10rpx 0;
	color: #4dbaee;
}

.more_body {
	width: 600rpx;
	background: #fff;
	border-radius: 20rpx;
	margin: 20rpx auto;
}

.current_font{
	font-size: 30rpx;
	margin: 20rpx;
}

.font_2{
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}

.current_font_2{
	margin: 10rpx 0;
}
</style>
