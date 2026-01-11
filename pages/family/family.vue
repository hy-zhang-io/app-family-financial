<template>
	<view class="content">
		<view class="header">
			<text class="title">家庭中心</text>
		</view>

		<view class="members-section">
			<text class="section-title">家庭成员</text>
			<scroll-view class="members-scroll" scroll-x>
				<view class="member-card active">
					<view class="avatar">我</view>
					<text class="member-name">我</text>
					<text class="member-role">管理员</text>
				</view>
			</scroll-view>
			<button class="add-member-btn" size="mini">+ 添加成员</button>
		</view>

		<view class="stats-section">
			<text class="section-title">家庭统计</text>
			<view class="stats-grid">
				<view class="stat-card">
					<text class="stat-icon">💰</text>
					<text class="stat-value">¥8,520</text>
					<text class="stat-label">总支出</text>
				</view>
				<view class="stat-card">
					<text class="stat-icon">👥</text>
					<text class="stat-value">1</text>
					<text class="stat-label">成员数</text>
				</view>
			</view>
		</view>

		<view class="radar-section">
			<text class="section-title">消费特征</text>
			<view class="radar-placeholder">
				<text class="placeholder-icon">📊</text>
				<text class="placeholder-text">雷达图区域</text>
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

.members-section,
.stats-section,
.radar-section {
	margin-bottom: 50rpx;
}

.section-title {
	display: block;
	font-size: 28rpx;
	color: rgba(255, 255, 255, 0.8);
	margin-bottom: 20rpx;
}

.members-scroll {
	white-space: nowrap;
	margin-bottom: 20rpx;
}

.member-card {
	display: inline-flex;
	flex-direction: column;
	align-items: center;
	gap: 10rpx;
	padding: 25rpx;
	margin-right: 20rpx;
	min-width: 130rpx;
	background: rgba(255, 255, 255, 0.05);
	border-radius: 20rpx;
	border: 2rpx solid transparent;
}

.member-card.active {
	background: rgba(79, 214, 200, 0.2);
	border-color: #4fd6c8;
}

.avatar {
	width: 80rpx;
	height: 80rpx;
	background: linear-gradient(135deg, #4fd6c8, #2d9c94);
	border-radius: 50%;
	display: flex;
	align-items: center;
	justify-content: center;
	color: #ffffff;
	font-size: 32rpx;
	font-weight: bold;
}

.member-name {
	font-size: 24rpx;
	color: #ffffff;
}

.member-role {
	font-size: 20rpx;
	color: rgba(255, 255, 255, 0.5);
}

.add-member-btn {
	background: rgba(255, 255, 255, 0.1);
	border: 1rpx dashed rgba(255, 255, 255, 0.3);
	border-radius: 30rpx;
	padding: 15rpx 40rpx;
	color: rgba(255, 255, 255, 0.7);
	font-size: 24rpx;
}

.stats-grid {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	gap: 20rpx;
}

.stat-card {
	background: rgba(255, 255, 255, 0.05);
	border-radius: 20rpx;
	padding: 30rpx;
	text-align: center;
}

.stat-icon {
	display: block;
	font-size: 48rpx;
	margin-bottom: 15rpx;
}

.stat-value {
	display: block;
	font-size: 32rpx;
	font-weight: bold;
	color: #4fd6c8;
	margin-bottom: 10rpx;
}

.stat-label {
	font-size: 22rpx;
	color: rgba(255, 255, 255, 0.6);
}

.radar-placeholder {
	height: 400rpx;
	background: rgba(255, 255, 255, 0.03);
	border-radius: 20rpx;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}

.placeholder-icon {
	font-size: 100rpx;
	margin-bottom: 20rpx;
}

.placeholder-text {
	font-size: 24rpx;
	color: rgba(255, 255, 255, 0.4);
}
</style>
