<template>
	<view class="content">
		<view class="header">
			<text class="title">预算规划</text>
		</view>

		<view class="budget-card">
			<text class="card-title">本月预算</text>
			<text class="budget-amount">¥15,000.00</text>
			<view class="progress-bar">
				<view class="progress-fill" style="width: 57%"></view>
			</view>
			<text class="budget-info">已使用 57% (¥8,520)</text>
		</view>

		<view class="prediction">
			<text class="section-title">现金流预测</text>
			<view class="chart-placeholder">
				<text class="placeholder-text">📈</text>
				<text class="placeholder-hint">图表区域</text>
			</view>
		</view>
	</view>
</template>

<script>
export default {

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
	margin-bottom: 40rpx;
	padding-top: 80rpx;
}

.title {
	font-size: 48rpx;
	font-weight: bold;
	color: #ffffff;
}

.budget-card {
	background: rgba(255, 255, 255, 0.05);
	backdrop-filter: blur(10px);
	border-radius: 30rpx;
	padding: 50rpx;
	margin-bottom: 40rpx;
	border: 1px solid rgba(255, 255, 255, 0.1);
}

.card-title {
	display: block;
	font-size: 24rpx;
	color: rgba(255, 255, 255, 0.6);
	margin-bottom: 20rpx;
}

.budget-amount {
	display: block;
	font-size: 56rpx;
	font-weight: bold;
	color: #4fd6c8;
	margin-bottom: 30rpx;
}

.progress-bar {
	height: 12rpx;
	background: rgba(255, 255, 255, 0.1);
	border-radius: 6rpx;
	overflow: hidden;
	margin-bottom: 15rpx;
}

.progress-fill {
	height: 100%;
	background: linear-gradient(90deg, #4fd6c8, #2d9c94);
	border-radius: 6rpx;
}

.budget-info {
	font-size: 22rpx;
	color: rgba(255, 255, 255, 0.5);
}

.prediction {
	background: rgba(255, 255, 255, 0.05);
	border-radius: 30rpx;
	padding: 40rpx;
	border: 1px solid rgba(255, 255, 255, 0.1);
}

.section-title {
	display: block;
	font-size: 28rpx;
	color: #ffffff;
	margin-bottom: 30rpx;
}

.chart-placeholder {
	height: 400rpx;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	background: rgba(255, 255, 255, 0.03);
	border-radius: 20rpx;
}

.placeholder-text {
	font-size: 80rpx;
	margin-bottom: 20rpx;
}

.placeholder-hint {
	font-size: 24rpx;
	color: rgba(255, 255, 255, 0.4);
}
</style>
