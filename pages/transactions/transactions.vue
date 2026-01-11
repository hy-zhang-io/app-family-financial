<template>
	<view class="content">
		<view class="header">
			<text class="title">交易记录</text>
		</view>

		<view class="filter-bar">
			<view class="month-selector">本月</view>
			<view class="filter-btn">筛选 🔍</view>
		</view>

		<view class="stats">
			<view class="stat-box">
				<text class="stat-label">收入</text>
				<text class="stat-value income">+¥10,000</text>
			</view>
			<view class="stat-box">
				<text class="stat-label">支出</text>
				<text class="stat-value expense">-¥8,520</text>
			</view>
		</view>

		<view class="transaction-list">
			<view class="empty-state">
				<text class="empty-icon">📝</text>
				<text class="empty-text">暂无交易记录</text>
				<text class="empty-hint">点击下方按钮开始记账</text>
			</view>
		</view>

		<view class="add-btn" @click="addRecord">+</view>
	</view>
</template>

<script>
export default {
	methods: {
		addRecord() {
			uni.showToast({
				title: '记账功能开发中',
				icon: 'none'
			})
		}
	}
}
</script>

<style scoped>
.content {
	min-height: 100vh;
	background: #0a0e27;
	padding: 40rpx;
	padding-bottom: 150rpx;
}

.header {
	margin-bottom: 30rpx;
	padding-top: 80rpx;
}

.title {
	font-size: 48rpx;
	font-weight: bold;
	color: #ffffff;
}

.filter-bar {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 30rpx;
}

.month-selector {
	padding: 15rpx 30rpx;
	background: rgba(255, 255, 255, 0.1);
	border-radius: 30rpx;
	color: #ffffff;
	font-size: 24rpx;
}

.filter-btn {
	padding: 15rpx 25rpx;
	background: rgba(79, 214, 200, 0.2);
	border-radius: 50%;
	font-size: 28rpx;
}

.stats {
	display: flex;
	gap: 20rpx;
	margin-bottom: 30rpx;
}

.stat-box {
	flex: 1;
	background: rgba(255, 255, 255, 0.05);
	border-radius: 20rpx;
	padding: 30rpx;
	text-align: center;
}

.stat-label {
	display: block;
	font-size: 22rpx;
	color: rgba(255, 255, 255, 0.6);
	margin-bottom: 10rpx;
}

.stat-value {
	display: block;
	font-size: 32rpx;
	font-weight: bold;
}

.income {
	color: #4fd6c8;
}

.expense {
	color: #ff6b6b;
}

.transaction-list {
	margin-top: 30rpx;
}

.empty-state {
	display: flex;
	flex-direction: column;
	align-items: center;
	padding: 100rpx 0;
}

.empty-icon {
	font-size: 120rpx;
	margin-bottom: 30rpx;
}

.empty-text {
	font-size: 32rpx;
	color: rgba(255, 255, 255, 0.8);
	margin-bottom: 15rpx;
}

.empty-hint {
	font-size: 24rpx;
	color: rgba(255, 255, 255, 0.5);
}

.add-btn {
	position: fixed;
	bottom: 150rpx;
	right: 40rpx;
	width: 100rpx;
	height: 100rpx;
	background: linear-gradient(135deg, #4fd6c8, #2d9c94);
	border-radius: 50%;
	display: flex;
	align-items: center;
	justify-content: center;
	font-size: 48rpx;
	color: #ffffff;
	box-shadow: 0 10rpx 30rpx rgba(79, 214, 200, 0.4);
}
</style>
