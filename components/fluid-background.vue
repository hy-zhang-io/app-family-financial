<template>
	<view class="fluid-container" :class="{ 'syncing': isSyncing }">
		<canvas
			class="fluid-canvas"
			:canvas-id="canvasId"
			:id="canvasId"
			:style="{ width: width + 'px', height: height + 'px' }"
		></canvas>
		<view class="fluid-overlay" :style="{ opacity: overlayOpacity }"></view>
		<!-- 数据同步时的光纤纹理效果 -->
		<view v-if="isSyncing" class="fiber-texture"></view>
	</view>
</template>

<script>
export default {
	name: 'FluidBackground',
	props: {
		// 健康状态: healthy(健康), warning(预警), crisis(危机)
		healthStatus: {
			type: String,
			default: 'healthy'
		},
		// 是否正在同步数据
		isSyncing: {
			type: Boolean,
			default: false
		},
		canvasId: {
			type: String,
			default: 'fluid-canvas'
		}
	},
	data() {
		return {
			width: 0,
			height: 0,
			ctx: null,
			animationId: null,
			particles: [],
			time: 0,
			overlayOpacity: 0.3
		}
	},
	mounted() {
		this.initCanvas()
	},
	beforeUnmount() {
		this.cancelAnimation()
	},
	watch: {
		healthStatus() {
			this.updateParticles()
		},
		isSyncing(newVal) {
			if (newVal) {
				this.startSyncEffect()
			} else {
				this.stopSyncEffect()
			}
		}
	},
	methods: {
		initCanvas() {
			const systemInfo = uni.getSystemInfoSync()
			this.width = systemInfo.windowWidth
			this.height = systemInfo.windowHeight

			this.$nextTick(() => {
				const ctx = uni.createCanvasContext(this.canvasId, this)
				this.ctx = ctx
				this.createParticles()
				this.startAnimation()
			})
		},
		createParticles() {
			this.particles = []
			const particleCount = 50

			for (let i = 0; i < particleCount; i++) {
				this.particles.push({
					x: Math.random() * this.width,
					y: Math.random() * this.height,
					radius: Math.random() * 100 + 50,
					vx: (Math.random() - 0.5) * 0.5,
					vy: (Math.random() - 0.5) * 0.5,
					phase: Math.random() * Math.PI * 2
				})
			}
		},
		updateParticles() {
			// 根据健康状态调整粒子速度和颜色
			const speedMultiplier = this.healthStatus === 'crisis' ? 3 :
								   this.healthStatus === 'warning' ? 2 : 1

			this.particles.forEach(p => {
				p.vx = (Math.random() - 0.5) * 0.5 * speedMultiplier
				p.vy = (Math.random() - 0.5) * 0.5 * speedMultiplier
			})
		},
		getGradientColors() {
			switch(this.healthStatus) {
				case 'healthy':
					return ['#0a3d2e', '#1a5f4a', '#4fd6c8']
				case 'warning':
					return ['#3d2e0a', '#5f4a1a', '#ffb347']
				case 'crisis':
					return ['#3d0a0a', '#5f1a1a', '#ff6b6b']
				default:
					return ['#0a0e27', '#1a2744', '#4fd6c8']
			}
		},
		draw() {
			if (!this.ctx) return

			const { ctx, width, height, time } = this
			const colors = this.getGradientColors()

			// 清空画布
			ctx.clearRect(0, 0, width, height)

			// 绘制背景渐变
			const gradient = ctx.createLinearGradient(0, 0, 0, height)
			gradient.addColorStop(0, colors[0])
			gradient.addColorStop(0.5, colors[1])
			gradient.addColorStop(1, colors[0])

			ctx.fillStyle = gradient
			ctx.fillRect(0, 0, width, height)

			// 绘制流体粒子
			this.particles.forEach((p, i) => {
				// 更新位置
				p.x += p.vx
				p.y += p.vy

				// 边界检测
				if (p.x < -p.radius) p.x = width + p.radius
				if (p.x > width + p.radius) p.x = -p.radius
				if (p.y < -p.radius) p.y = height + p.radius
				if (p.y > height + p.radius) p.y = -p.radius

				// 计算呼吸效果
				const breathe = Math.sin(time * 0.001 + p.phase) * 20
				const currentRadius = p.radius + breathe

				// 绘制粒子
				const particleGradient = ctx.createRadialGradient(
					p.x, p.y, 0,
					p.x, p.y, currentRadius
				)

				const alpha = this.isSyncing ? 0.3 : 0.15
				particleGradient.addColorStop(0, this.hexToRgba(colors[2], alpha))
				particleGradient.addColorStop(1, this.hexToRgba(colors[2], 0))

				ctx.fillStyle = particleGradient
				ctx.beginPath()
				ctx.arc(p.x, p.y, currentRadius, 0, Math.PI * 2)
				ctx.fill()
			})

			// 数据同步时的光纤效果
			if (this.isSyncing) {
				this.drawFiberEffect(ctx, width, height, time)
			}

			ctx.draw()
			this.time += 16
		},
		drawFiberEffect(ctx, width, height, time) {
			const lineCount = 10
			const colors = this.getGradientColors()

			for (let i = 0; i < lineCount; i++) {
				const y = (height / lineCount) * i + Math.sin(time * 0.005 + i) * 50

				ctx.strokeStyle = this.hexToRgba(colors[2], 0.3)
				ctx.lineWidth = 2
				ctx.beginPath()
				ctx.moveTo(0, y)

				for (let x = 0; x < width; x += 10) {
					const waveY = y + Math.sin(x * 0.02 + time * 0.01) * 20
					ctx.lineTo(x, waveY)
				}

				ctx.stroke()
			}
		},
		startAnimation() {
			const animate = () => {
				this.draw()
				this.animationId = requestAnimationFrame(animate)
			}
			animate()
		},
		cancelAnimation() {
			if (this.animationId) {
				cancelAnimationFrame(this.animationId)
				this.animationId = null
			}
		},
		startSyncEffect() {
			this.overlayOpacity = 0.1
		},
		stopSyncEffect() {
			this.overlayOpacity = 0.3
		},
		hexToRgba(hex, alpha) {
			const r = parseInt(hex.slice(1, 3), 16)
			const g = parseInt(hex.slice(3, 5), 16)
			const b = parseInt(hex.slice(5, 7), 16)
			return `rgba(${r}, ${g}, ${b}, ${alpha})`
		}
	}
}
</script>

<style lang="scss" scoped>
.fluid-container {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	z-index: -1;
	overflow: hidden;

	&.syncing {
		animation: pulse 1s ease-in-out infinite;
	}
}

.fluid-canvas {
	display: block;
}

.fluid-overlay {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background: radial-gradient(circle at center, transparent 0%, rgba(0, 0, 0, 0.5) 100%);
	pointer-events: none;
}

.fiber-texture {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background: repeating-linear-gradient(
		90deg,
		transparent,
		transparent 10px,
		rgba(79, 214, 200, 0.1) 10px,
		rgba(79, 214, 200, 0.1) 20px
	);
	animation: fiberFlow 0.5s linear infinite;
	pointer-events: none;
}

@keyframes pulse {
	0%, 100% {
		opacity: 1;
	}
	50% {
		opacity: 0.8;
	}
}

@keyframes fiberFlow {
	0% {
		transform: translateX(0);
	}
	100% {
		transform: translateX(20px);
	}
}
</style>
