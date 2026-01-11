# 流体金融家庭财务APP

基于流体设计语言的 uni-app 家庭财务管理应用。

## 项目特点

### 视觉设计
- **动态流体背景** - 根据财务健康状况实时变化的背景效果
- **全息玻璃拟态** - 深度感与层次分明的设计语言
- **可变字体** - 自适应阅读环境的字体系统
- **无障碍设计** - 内置色盲模式和银发关怀模式

### 核心功能
1. **财富全景窗 (首页)**
   - 3D交互式财富之树
   - 财务天气Widget
   - 家庭成员头像堆叠
   - 语音记账功能

2. **交易流 (生活足迹)**
   - 时间轴式交易展示
   - 来源标识 (微信/支付宝/手动)
   - 智能分类修正
   - 高级筛选功能

3. **规划与预算 (未来模拟器)**
   - 现金流预测曲线
   - 时间穿越交互
   - 假设推演功能
   - 分类预算管理

4. **资产与数据 (数据枢纽)**
   - 微信/支付宝账单导入
   - 数据导出 (Excel/PDF/JSON)
   - 本地加密备份
   - 智能数据清洗

5. **家庭中心 (共治看板)**
   - 成员消费特征雷达图
   - 支出对比分析
   - 实时同步状态
   - 家庭成员管理

### AI智能体
- 右下角常驻金融球体
- 智能导入建议
- 数据归档提醒
- 分类确认询问

## 技术栈

- **框架**: uni-app (Vue 3)
- **UI**: 自定义流体设计系统
- **存储**: 本地 Storage
- **图表**: Canvas 自绘
- **动画**: CSS3 + Canvas

## 项目结构

```
app-familyfinancial/
├── components/           # 全局组件
│   ├── fluid-background.vue   # 流体背景组件
│   └── ai-agent.vue           # AI智能体组件
├── pages/                # 页面
│   ├── index/           # 首页-财富全景窗
│   ├── transactions/    # 交易流页面
│   ├── budget/          # 规划与预算页面
│   ├── assets/          # 资产与数据管理页面
│   └── family/          # 家庭中心页面
├── static/              # 静态资源
│   └── tabbar/          # 底部导航图标
├── App.vue             # 应用入口
├── main.js             # 主文件
├── pages.json          # 页面配置
├── manifest.json       # 应用配置
└── uni.scss           # 全局样式变量

```

## 设计规范

### 色彩系统
- **主题色**: #4fd6c8 (极光绿)
- **健康状态**: #0a3d2e - #1a5f4a - #4fd6c8
- **预警状态**: #3d2e0a - #5f4a1a - #ffb347
- **危机状态**: #3d0a0a - #5f1a1a - #ff6b6b

### 交互范式
- **语音记账**: 打开App即进入聆听状态
- **情境感知**: 基于地理位置的速记卡片
- **手势操作**: 捏合预算、时间穿越滑动
- **眼动追踪**: 注视展开详情

### 无障碍规范
- 内置自适应色盲模式
- 银发关怀模式 (大字高对比)
- 图标+纹理双重信息传达
- 生物识别安全验证

## 开发说明

### 环境要求
- Node.js 14+
- HBuilderX 或 Vue CLI
- uni-app CLI

### 安装依赖
```bash
npm install
```

### 运行项目
```bash
# HBuilderX
# 直接运行到浏览器/模拟器/真机

# CLI
npm run dev:h5
npm run dev:mp-weixin
npm run dev:app
```

### TabBar图标
需要在 `static/tabbar/` 目录下放置以下图标:
- home.png / home-active.png
- transactions.png / transactions-active.png
- budget.png / budget-active.png
- assets.png / assets-active.png
- family.png / family-active.png

建议尺寸: 81x81px, PNG格式, 透明背景

## 核心功能实现

### 数据导入
1. 微信/支付宝 CSV 账单解析
2. 智能商户分类映射
3. 自动去重处理
4. 不确定账单AI辅助分类

### 数据导出
1. Excel 格式 (带水印)
2. PDF 可视化报告
3. 加密 JSON (用于迁移)
4. 生物识别验证

### AI智能交互
1. 语音意图识别
2. 自然语言金额提取
3. 智能分类推荐
4. 主动服务提醒

## 待完善功能

- [ ] 真实的语音识别集成
- [ ] 实际的微信/支付宝 API 对接
- [ ] PDF 报告生成
- [ ] 云端备份同步
- [ ] 家庭成员实时协作
- [ ] 眼动追踪交互
- [ ] 3D 财富之树 WebGL 实现
- [ ] 更多图表类型

## 许可证

MIT License

## 作者

Hon-Yu Zhang

GLM Coding
