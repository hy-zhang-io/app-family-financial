<template>
	<view class="ai-agent-container">
		<!-- AI球体 -->
		<view
			class="ai-sphere"
			:class="{
				'pulsing': isPulsing,
				'spinning': isProcessing
			}"
			:style="{
				width: size + 'rpx',
				height: size + 'rpx',
				background: sphereGradient
			}"
			@click="handleClick"
		>
			<!-- 球体内部纹理 -->
			<view class="sphere-inner" v-if="isProcessing">
				<view class="spin-ring"></view>
			</view>

			<!-- 状态指示器 -->
			<view class="status-indicator" :class="statusClass"></view>
		</view>

		<!-- 消息气泡 -->
		<view
			v-if="message"
			class="message-bubble"
			:class="{ 'show': message }"
		>
			<text class="message-text">{{ message }}</text>
			<view class="message-actions" v-if="showActions">
				<button
					v-for="(action, index) in actions"
					:key="index"
					class="action-btn"
					size="mini"
					@click="handleAction(action)"
				>
					{{ action.label }}
				</button>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	name: 'AIAgent',
	props: {
		size: {
			type: Number,
			default: 100
		},
		// 财务健康分数 (0-100)
		healthScore: {
			type: Number,
			default: 75
		},
		isProcessing: {
			type: Boolean,
			default: false
		}
	},
	data() {
		return {
			isPulsing: false,
			message: '',
			showActions: false,
			actions: [],
			pulseInterval: null
		}
	},
	computed: {
		statusClass() {
			if (this.isProcessing) return 'processing'
			if (this.healthScore >= 70) return 'healthy'
			if (this.healthScore >= 40) return 'warning'
			return 'danger'
		},
		sphereGradient() {
			const score = this.healthScore
			let color1, color2

			if (score >= 70) {
				color1 = '#4fd6c8'
				color2 = '#2d9c94'
			} else if (score >= 40) {
				color1 = '#ffb347'
				color2 = '#ff8c00'
			} else {
				color1 = '#ff6b6b'
				color2 = '#cc4444'
			}

			return `linear-gradient(135deg, ${color1} 0%, ${color2} 100%)`
		},
		pulseSpeed() {
			const score = this.healthScore
			if (score >= 70) return 2000
			if (score >= 40) return 1500
			return 800
		}
	},
	mounted() {
		this.startPulse()
	},
	beforeUnmount() {
		this.stopPulse()
	},
	methods: {
		startPulse() {
			this.pulseInterval = setInterval(() => {
				this.isPulsing = true
				setTimeout(() => {
					this.isPulsing = false
				}, 300)
			}, this.pulseSpeed)
		},
		stopPulse() {
			if (this.pulseInterval) {
				clearInterval(this.pulseInterval)
				this.pulseInterval = null
			}
		},
		handleClick() {
			this.$emit('click')
			// 显示默认提示
			if (!this.message) {
				this.showMessage('我是您的财务助手，有什么可以帮您吗？')
			}
		},
		showMessage(msg, actions = null) {
			this.message = msg
			this.showActions = !!actions
			this.actions = actions || []

			// 3秒后自动隐藏
			setTimeout(() => {
				this.hideMessage()
			}, 5000)
		},
		hideMessage() {
			this.message = ''
			this.showActions = false
			this.actions = []
		},
		handleAction(action) {
			this.$emit('action', action)
			this.hideMessage()
		},
		// 智能导入建议
		suggestImport(sourceType) {
			const sourceName = sourceType === 'wechat' ? '微信' : '支付宝'
			this.showMessage(
				`我发现了一份未记录的${sourceName}账单，需要我为您导入并清洗吗？`,
				[
					{ label: '立即导入', value: 'import', source: sourceType },
					{ label: '稍后再说', value: 'later' }
				]
			)
			// 高频脉冲
			this.isPulsing = true
			setTimeout(() => {
				this.isPulsing = false
			}, 2000)
		},
		// 数据归档提醒
		suggestArchive() {
			this.showMessage(
				'建议为您创建一次数据快照，保护您的财务数据。',
				[
					{ label: '立即备份', value: 'backup' },
					{ label: '稍后提醒', value: 'remind' }
				]
			)
		},
		// 分类确认询问
		confirmCategory(merchantName) {
			this.showMessage(
				`"${merchantName}" 是在超市购物吗？`,
				[
					{ label: '是', value: 'confirm', category: '购物' },
					{ label: '否', value: 'deny' }
				]
			)
		},
		// 显示成功消息
		showSuccess(msg) {
			this.showMessage(msg)
			// 成功时的动画效果
			this.isPulsing = true
			setTimeout(() => {
				this.isPulsing = false
			}, 500)
		},
		// 显示错误消息
		showError(msg) {
			this.showMessage(msg)
		}
	}
}
</script>

<style lang="scss" scoped>
.ai-agent-container {
	position: fixed;
	bottom: 180rpx;
	right: 30rpx;
	z-index: 999;
}

.ai-sphere {
	position: relative;
	border-radius: 50%;
	box-shadow: 0 8rpx 30rpx rgba(0, 0, 0, 0.3),
				inset 0 -10rpx 20rpx rgba(0, 0, 0, 0.2),
				inset 0 10rpx 20rpx rgba(255, 255, 255, 0.3);
	cursor: pointer;
	transition: all 0.3s ease;
	animation: float 3s ease-in-out infinite;

	&::before {
		content: '';
		position: absolute;
		top: 10%;
		left: 20%;
		width: 30%;
		height: 30%;
		background: radial-gradient(circle, rgba(255, 255, 255, 0.4) 0%, transparent 70%);
		border-radius: 50%;
	}

	&.pulsing {
		animation: pulse-scale 0.6s ease-in-out;
	}

	&.spinning {
		animation: spin 1s linear infinite;
	}

	&:active {
		transform: scale(0.95);
	}
}

.sphere-inner {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	width: 80%;
	height: 80%;
}

.spin-ring {
	width: 100%;
	height: 100%;
	border: 4rpx solid rgba(255, 255, 255, 0.3);
	border-top-color: rgba(255, 255, 255, 0.9);
	border-radius: 50%;
	animation: spin-ring 1s linear infinite;
}

.status-indicator {
	position: absolute;
	bottom: 0;
	right: 0;
	width: 24rpx;
	height: 24rpx;
	border-radius: 50%;
	border: 3rpx solid #fff;

	&.healthy {
		background: #4fd6c8;
		box-shadow: 0 0 10rpx #4fd6c8;
	}

	&.warning {
		background: #ffb347;
		box-shadow: 0 0 10rpx #ffb347;
	}

	&.danger {
		background: #ff6b6b;
		box-shadow: 0 0 10rpx #ff6b6b;
	}

	&.processing {
		background: #ffffff;
		box-shadow: 0 0 10rpx #ffffff;
		animation: blink 0.5s ease-in-out infinite;
	}
}

.message-bubble {
	position: absolute;
	bottom: 120rpx;
	right: 0;
	width: 400rpx;
	background: rgba(255, 255, 255, 0.95);
	backdrop-filter: blur(20rpx);
	border-radius: 20rpx;
	padding: 25rpx;
	box-shadow: 0 10rpx 40rpx rgba(0, 0, 0, 0.2);
	transform-origin: bottom right;
	opacity: 0;
	transform: scale(0.8);
	transition: all 0.3s ease;
	pointer-events: none;

	&.show {
		opacity: 1;
		transform: scale(1);
		pointer-events: auto;
	}

	&::before {
		content: '';
		position: absolute;
		bottom: -10rpx;
		right: 40rpx;
		width: 0;
		height: 0;
		border-left: 15rpx solid transparent;
		border-right: 15rpx solid transparent;
		border-top: 15rpx solid rgba(255, 255, 255, 0.95);
	}
}

.message-text {
	display: block;
	color: #0a0e27;
	font-size: 26rpx;
	line-height: 1.6;
	margin-bottom: 15rpx;
}

.message-actions {
	display: flex;
	gap: 10rpx;
	margin-top: 15rpx;
}

.action-btn {
	flex: 1;
	background: linear-gradient(135deg, #4fd6c8 0%, #2d9c94 100%);
	color: #fff;
	border: none;
	border-radius: 30rpx;
	font-size: 24rpx;
	padding: 10rpx 20rpx;

	&:active {
		opacity: 0.8;
	}
}

@keyframes float {
	0%, 100% {
		transform: translateY(0);
	}
	50% {
		transform: translateY(-10rpx);
	}
}

@keyframes pulse-scale {
	0%, 100% {
		transform: scale(1);
	}
	50% {
		transform: scale(1.1);
	}
}

@keyframes spin {
	0% {
		transform: rotate(0deg);
	}
	100% {
		transform: rotate(360deg);
	}
}

@keyframes spin-ring {
	0% {
		transform: rotate(0deg);
	}
	100% {
		transform: rotate(360deg);
	}
}

@keyframes blink {
	0%, 100% {
		opacity: 1;
	}
	50% {
		opacity: 0.3;
	}
}
</style>
