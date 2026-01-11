# HBuilderX 运行问题修复指南

## 问题原因
HBuilderX 需要项目文件在根目录，而不是在 `src` 目录中。

## 解决方案

### 方法一: 恢复项目结构（推荐）

1. **停止所有运行的服务**
   - 关闭浏览器中打开的 localhost:8080
   - 在命令行中按 Ctrl+C 停止开发服务器

2. **恢复文件到根目录**
   在项目根目录执行:
   ```bash
   # Windows PowerShell
   move src\pages .\
   move src\components .\
   move src\static .\
   move src\App.vue .\
   move src\main.js .\
   move src\index.html .\
   move src\manifest.json .\
   move src\pages.json .\
   move src\uni.scss .\
   move src\uni.promisify.adaptor.js .\
   rmdir src
   ```

3. **在 HBuilderX 中重新运行**
   - 右键项目 → 运行 → 运行到浏览器

### 方法二: 重新创建项目（最简单）

如果上面的方法不行，建议：

1. **在 HBuilderX 中创建新项目**
   - 文件 → 新建 → 项目
   - 选择 `uni-app` → `Vue3/Vite` 版本
   - 项目名称: `familyfinance-new`
   - 模板: `默认模板`

2. **复制文件到新项目**
   将以下文件复制到新项目对应位置:
   - `pages/` → 新项目的 `pages/`
   - `components/` → 新项目的 `components/`
   - `static/` → 新项目的 `static/`
   - `App.vue` → 新项目的根目录
   - `pages.json` → 新项目的根目录
   - `manifest.json` → 新项目的根目录
   - `uni.scss` → 新项目的根目录

### 方法三: 修改 vite.config.js（临时方案）

如果要保持当前结构，修改 `vite.config.js`:

```javascript
import { defineConfig } from 'vite'
import uni from '@dcloudio/vite-plugin-uni'

export default defineConfig({
  plugins: [uni()],
  server: {
    port: 8080,
    host: '0.0.0.0'
  },
  // 添加根目录配置
  root: './src'
})
```

## HBuilderX 正确的项目结构

```
app-familyfinancial/
├── pages/              # 页面文件夹
│   ├── index/
│   ├── transactions/
│   ├── budget/
│   ├── assets/
│   └── family/
├── components/         # 组件文件夹
│   ├── fluid-background.vue
│   └── ai-agent.vue
├── static/            # 静态资源
│   └── tabbar/
├── App.vue            # 应用入口
├── main.js            # 主文件
├── pages.json         # 页面配置
├── manifest.json      # 应用配置
├── uni.scss          # 全局样式
└── index.html        # HTML模板
```

## 验证方法

在 HBuilderX 中运行后应该看到:
- 控制台显示编译成功
- 浏览器自动打开
- 显示流体金融APP界面

## 常见错误

### 404 错误
- 原因: 文件结构不正确
- 解决: 确保 pages.json 中的路径与实际文件位置一致

### 空白页面
- 原因: 组件未正确引入
- 解决: 检查 App.vue 和页面中的组件导入路径

### TabBar 不显示
- 原因: 缺少图标文件
- 解决: 在 static/tabbar/ 添加图标或删除 pages.json 中的 tabBar 配置
