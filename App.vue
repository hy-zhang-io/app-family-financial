<script>
	export default {
		onLaunch: function() {
			console.log('流体金融 App Launch')
			// 初始化应用配置
			this.initApp()
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
		methods: {
			initApp() {
				// 初始化本地存储
				if (!uni.getStorageSync('transactions')) {
					uni.setStorageSync('transactions', [])
				}
				if (!uni.getStorageSync('categories')) {
					uni.setStorageSync('categories', [
						{ id: 1, name: '餐饮', icon: '🍜', color: '#ff6b6b' },
						{ id: 2, name: '交通', icon: '🚗', color: '#4ecdc4' },
						{ id: 3, name: '购物', icon: '🛒', color: '#ffe66d' },
						{ id: 4, name: '娱乐', icon: '🎮', color: '#95e1d3' },
						{ id: 5, name: '医疗', icon: '💊', color: '#ff8b94' },
						{ id: 6, name: '教育', icon: '📚', color: '#a8e6cf' },
						{ id: 7, name: '居住', icon: '🏠', color: '#ffd3b6' },
						{ id: 8, name: '其他', icon: '📦', color: '#c7ceea' }
					])
				}
				if (!uni.getStorageSync('budgets')) {
					uni.setStorageSync('budgets', {})
				}
				if (!uni.getStorageSync('familyMembers')) {
					uni.setStorageSync('familyMembers', [
						{ id: 1, name: '我', avatar: '', role: 'admin' }
					])
				}
				if (!uni.getStorageSync('assets')) {
					uni.setStorageSync('assets', {
						total: 0,
						accounts: []
					})
				}
				if (!uni.getStorageSync('settings')) {
					uni.setStorageSync('settings', {
						accessibilityMode: false,
						highContrastMode: false,
						animationEnabled: true,
						voiceInputEnabled: true
					})
				}
			}
		}
	}
</script>

<style lang="scss">
	/* 全局样式 */
	@import '@/uni.scss';

	page {
		background-color: #0a0e27;
		color: #ffffff;
		font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
	}

	/* 全息玻璃拟态效果 */
	.glass-effect {
		background: rgba(255, 255, 255, 0.1);
		backdrop-filter: blur(10px);
		-webkit-backdrop-filter: blur(10px);
		border: 1px solid rgba(255, 255, 255, 0.2);
		border-radius: 20rpx;
	}

	/* 高对比度模式 */
	.high-contrast {
		filter: contrast(1.2);
	}

	/* 银发关怀模式 */
	.silver-mode {
		font-size: 40rpx;
		line-height: 1.8;
	}

	.silver-mode .glass-effect {
		background: rgba(255, 255, 255, 0.95);
		backdrop-filter: none;
		border: 2px solid #000;
	}

	/* 发光效果 */
	.glow {
		text-shadow: 0 0 10px rgba(79, 214, 200, 0.5);
	}

	.glow-card {
		box-shadow: 0 0 20px rgba(79, 214, 200, 0.3);
	}

	/* 通用按钮样式 */
	.btn-fluid {
		background: linear-gradient(135deg, #4fd6c8 0%, #2d9c94 100%);
		border-radius: 50rpx;
		color: #fff;
		padding: 20rpx 40rpx;
		border: none;
		box-shadow: 0 4rpx 15rpx rgba(79, 214, 200, 0.3);
		transition: all 0.3s ease;
	}

	.btn-fluid:active {
		transform: scale(0.95);
		box-shadow: 0 2rpx 10rpx rgba(79, 214, 200, 0.5);
	}

	/* 通用卡片样式 */
	.card-fluid {
		background: rgba(255, 255, 255, 0.08);
		backdrop-filter: blur(10px);
		border-radius: 20rpx;
		padding: 30rpx;
		margin-bottom: 20rpx;
		border: 1px solid rgba(255, 255, 255, 0.1);
	}

	/* 文本颜色工具类 */
	.text-primary {
		color: #4fd6c8;
	}

	.text-warning {
		color: #ffb347;
	}

	.text-danger {
		color: #ff6b6b;
	}

	.text-success {
		color: #4ecdc4;
	}

	.text-secondary {
		color: #8b9dc3;
	}

	/* 间距工具类 */
	.mt-10 { margin-top: 10rpx; }
	.mt-20 { margin-top: 20rpx; }
	.mt-30 { margin-top: 30rpx; }
	.mb-10 { margin-bottom: 10rpx; }
	.mb-20 { margin-bottom: 20rpx; }
	.mb-30 { margin-bottom: 30rpx; }
	.ml-10 { margin-left: 10rpx; }
	.mr-10 { margin-right: 10rpx; }
	.p-20 { padding: 20rpx; }
	.p-30 { padding: 30rpx; }
</style>
