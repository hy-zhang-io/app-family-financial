<template>
	<view class="content">
		<view class="header">
			<text class="title">流体金融家庭财务</text>
			<text class="subtitle">Fluid Finance Family App</text>
		</view>

		<view class="card">
			<text class="card-title">总资产</text>
			<text class="amount">¥128,500.00</text>
			<text class="change">📈 +8.5% 较上月</text>
		</view>

		<view class="stats">
			<view class="stat-item">
				<text class="stat-label">本月支出</text>
				<text class="stat-value">¥8,520.00</text>
			</view>
			<view class="stat-item">
				<text class="stat-label">本月预算</text>
				<text class="stat-value">¥15,000.00</text>
			</view>
		</view>

		<view class="health-status">
			<text class="status-icon">☀️</text>
			<text class="status-text">财务状况：健康</text>
		</view>

		<view class="actions">
			<button class="btn" @click="addRecord">记一笔</button>
			<button class="btn btn-outline" @click="viewReport">查看报表</button>
		</view>
	</view>
</template>

<script>
export default {
	data() {
		return {

		}
	},
	onLoad() {
		console.log('Index page loaded')
	},
	methods: {
		addRecord() {
			uni.showToast({
				title: '记账功能开发中',
				icon: 'none'
			})
		},
		viewReport() {
			uni.switchTab({
				url: '/pages/budget/budget'
			})
		}
	}
}
</script>

<style scoped>
.content {
	min-height: 100vh;
	background: linear-gradient(135deg, #0a3d2e 0%, #1a5f4a 50%, #4fd6c8 100%);
	padding: 40rpx;
}

.header {
	text-align: center;
	margin-bottom: 60rpx;
	padding-top: 100rpx;
}

.title {
	display: block;
	font-size: 48rpx;
	font-weight: bold;
	color: #ffffff;
	margin-bottom: 10rpx;
}

.subtitle {
	font-size: 24rpx;
	color: rgba(255, 255, 255, 0.7);
}

.card {
	background: rgba(255, 255, 255, 0.15);
	backdrop-filter: blur(10px);
	border-radius: 30rpx;
	padding: 50rpx;
	text-align: center;
	margin-bottom: 40rpx;
	border: 1px solid rgba(255, 255, 255, 0.2);
}

.card-title {
	display: block;
	font-size: 26rpx;
	color: rgba(255, 255, 255, 0.8);
	margin-bottom: 20rpx;
}

.amount {
	display: block;
	font-size: 64rpx;
	font-weight: bold;
	color: #4fd6c8;
	text-shadow: 0 0 20px rgba(79, 214, 200, 0.5);
	margin-bottom: 15rpx;
}

.change {
	font-size: 24rpx;
	color: #4fd6c8;
}

.stats {
	display: flex;
	gap: 20rpx;
	margin-bottom: 40rpx;
}

.stat-item {
	flex: 1;
	background: rgba(255, 255, 255, 0.1);
	backdrop-filter: blur(10px);
	border-radius: 20rpx;
	padding: 30rpx;
	text-align: center;
	border: 1px solid rgba(255, 255, 255, 0.15);
}

.stat-label {
	display: block;
	font-size: 22rpx;
	color: rgba(255, 255, 255, 0.7);
	margin-bottom: 10rpx;
}

.stat-value {
	display: block;
	font-size: 32rpx;
	font-weight: bold;
	color: #ffffff;
}

.health-status {
	display: flex;
	align-items: center;
	justify-content: center;
	gap: 15rpx;
	background: rgba(255, 255, 255, 0.1);
	backdrop-filter: blur(10px);
	border-radius: 50rpx;
	padding: 25rpx 50rpx;
	margin-bottom: 40rpx;
	border: 1px solid rgba(255, 255, 255, 0.15);
}

.status-icon {
	font-size: 40rpx;
}

.status-text {
	font-size: 26rpx;
	color: #ffffff;
}

.actions {
	display: flex;
	gap: 20rpx;
}

.btn {
	flex: 1;
	height: 90rpx;
	line-height: 90rpx;
	background: linear-gradient(135deg, #4fd6c8, #2d9c94);
	border-radius: 50rpx;
	color: #ffffff;
	font-size: 28rpx;
	border: none;
	box-shadow: 0 10rpx 30rpx rgba(79, 214, 200, 0.3);
}

.btn-outline {
	flex: 1;
	height: 90rpx;
	line-height: 90rpx;
	background: transparent;
	border: 2rpx solid rgba(255, 255, 255, 0.3);
	border-radius: 50rpx;
	color: #ffffff;
	font-size: 28rpx;
}
</style>
