<template>
	<view class="content">
		<view class="header">
			<text class="title">数据管理</text>
		</view>

		<view class="section">
			<text class="section-title">资金源连接</text>
			<view class="account-list">
				<view class="account-item">
					<view class="account-icon wechat">💬</view>
					<view class="account-info">
						<text class="account-name">微信支付</text>
						<text class="account-status">未连接</text>
					</view>
					<button class="connect-btn" size="mini">连接</button>
				</view>
				<view class="account-item">
					<view class="account-icon alipay">💳</view>
					<view class="account-info">
						<text class="account-name">支付宝</text>
						<text class="account-status">未连接</text>
					</view>
					<button class="connect-btn" size="mini">连接</button>
				</view>
			</view>
		</view>

		<view class="section">
			<text class="section-title">数据保险箱</text>
			<view class="data-actions">
				<button class="action-btn" @click="exportData">📤 导出数据</button>
				<button class="action-btn" @click="importData">📥 导入数据</button>
				<button class="action-btn" @click="backupData">💾 创建备份</button>
			</view>
		</view>

		<view class="section">
			<text class="section-title">数据统计</text>
			<view class="stats-grid">
				<view class="stat-box">
					<text class="stat-value">0</text>
					<text class="stat-label">交易数</text>
				</view>
				<view class="stat-box">
					<text class="stat-value">8</text>
					<text class="stat-label">分类数</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	methods: {
		exportData() {
			uni.showToast({
				title: '导出功能开发中',
				icon: 'none'
			})
		},
		importData() {
			uni.showToast({
				title: '导入功能开发中',
				icon: 'none'
			})
		},
		backupData() {
			uni.showToast({
				title: '备份功能开发中',
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
	margin-bottom: 40rpx;
	padding-top: 80rpx;
}

.title {
	font-size: 48rpx;
	font-weight: bold;
	color: #ffffff;
}

.section {
	margin-bottom: 50rpx;
}

.section-title {
	display: block;
	font-size: 28rpx;
	color: rgba(255, 255, 255, 0.8);
	margin-bottom: 20rpx;
}

.account-list {
	display: flex;
	flex-direction: column;
	gap: 20rpx;
}

.account-item {
	display: flex;
	align-items: center;
	gap: 20rpx;
	background: rgba(255, 255, 255, 0.05);
	border-radius: 20rpx;
	padding: 30rpx;
}

.account-icon {
	width: 70rpx;
	height: 70rpx;
	display: flex;
	align-items: center;
	justify-content: center;
	border-radius: 15rpx;
	font-size: 36rpx;
}

.wechat {
	background: rgba(76, 175, 80, 0.2);
}

.alipay {
	background: rgba(33, 150, 243, 0.2);
}

.account-info {
	flex: 1;
}

.account-name {
	display: block;
	font-size: 28rpx;
	color: #ffffff;
	margin-bottom: 5rpx;
}

.account-status {
	font-size: 22rpx;
	color: rgba(255, 255, 255, 0.5);
}

.connect-btn {
	background: linear-gradient(135deg, #4fd6c8, #2d9c94);
	color: #ffffff;
	border: none;
	border-radius: 30rpx;
	padding: 10rpx 30rpx;
	font-size: 22rpx;
}

.data-actions {
	display: flex;
	flex-direction: column;
	gap: 15rpx;
}

.action-btn {
	background: rgba(255, 255, 255, 0.05);
	border: 1px solid rgba(255, 255, 255, 0.1);
	border-radius: 15rpx;
	padding: 30rpx;
	color: #ffffff;
	font-size: 26rpx;
	text-align: left;
}

.stats-grid {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	gap: 20rpx;
}

.stat-box {
	background: rgba(255, 255, 255, 0.05);
	border-radius: 20rpx;
	padding: 40rpx;
	text-align: center;
}

.stat-value {
	display: block;
	font-size: 40rpx;
	font-weight: bold;
	color: #4fd6c8;
	margin-bottom: 10rpx;
}

.stat-label {
	font-size: 22rpx;
	color: rgba(255, 255, 255, 0.6);
}
</style>
