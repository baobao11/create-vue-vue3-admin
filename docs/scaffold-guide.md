# Vue3 Admin 脚手架搭建指南

## 📋 项目概述

这是一个基于 Vue 3 + TypeScript + Vite 的现代化管理后台脚手架，集成了完整的开发工具链和最佳实践。

## 🛠 技术栈

### 核心框架

- **Vue 3.5.18** - 渐进式 JavaScript 框架
- **TypeScript 5.8.3** - JavaScript 的超集，提供类型安全
- **Vite 7.0.6** - 下一代前端构建工具
- **Vue Router 4.5.1** - Vue.js 官方路由管理器
- **Pinia 3.0.3** - Vue 的状态管理库

### UI 组件库

- **Element Plus 2.10.4** - 基于 Vue 3 的组件库
- **自动按需导入** - 优化打包体积

### 开发工具

- **ESLint 9.32.0** - JavaScript 代码检查工具
- **Prettier 3.6.2** - 代码格式化工具
- **Stylelint 16.22.0** - CSS/SCSS 代码检查工具
- **Husky 9.1.7** - Git hooks 工具
- **lint-staged 16.1.2** - 暂存文件 lint 工具

### 代码规范

- **@commitlint/cli 19.8.1** - Git 提交信息规范检查
- **@commitlint/config-conventional 19.8.1** - 约定式提交规范

## 📁 项目结构

```
vue3-admin/
├── .vscode/                    # VS Code 配置
│   ├── settings.json           # 编辑器设置
│   └── extensions.json         # 推荐扩展
├── .husky/                     # Git hooks
│   ├── commit-msg              # 提交信息检查
│   └── pre-commit              # 提交前代码检查
├── docs/                       # 项目文档
│   ├── commit-convention.md    # Git 提交规范
│   └── scaffold-guide.md       # 脚手架搭建指南
├── src/                        # 源代码
│   ├── assets/                 # 静态资源
│   ├── components/             # 公共组件
│   ├── router/                 # 路由配置
│   ├── stores/                 # 状态管理
│   ├── styles/                 # 样式文件
│   │   └── element-variables.scss  # Element Plus 主题变量
│   ├── views/                  # 页面组件
│   ├── App.vue                 # 根组件
│   └── main.ts                 # 入口文件
├── .editorconfig               # 编辑器配置
├── .eslintrc.cjs              # ESLint 配置
├── .prettierrc.json           # Prettier 配置
├── commitlint.config.js        # Commitlint 配置
├── stylelint.config.cjs        # Stylelint 配置
├── tsconfig.json              # TypeScript 配置
├── vite.config.ts             # Vite 配置
└── package.json               # 项目配置
```

## 🚀 快速开始

### 环境要求

- Node.js >= 18.0.0 (推荐 20+)
- pnpm >= 8.0.0

### 安装依赖

```bash
pnpm install
```

### 启动开发服务器

```bash
pnpm dev
```

### 构建生产版本

```bash
pnpm build
```

### 代码检查

```bash
pnpm lint
```

## ⚙️ 配置说明

### 1. Vite 配置 (vite.config.ts)

```typescript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  plugins: [
    vue(),
    // 自动导入 Vue API
    AutoImport({
      imports: ['vue', 'vue-router'],
      resolvers: [ElementPlusResolver()],
      dts: 'src/auto-imports.d.ts',
    }),
    // 自动导入组件
    Components({
      resolvers: [ElementPlusResolver()],
      dts: 'src/components.d.ts',
    }),
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url)),
    },
  },
})
```

### 2. TypeScript 配置 (tsconfig.json)

```json
{
  "extends": "@vue/tsconfig/tsconfig.dom.json",
  "include": ["env.d.ts", "src/**/*", "src/**/*.vue"],
  "exclude": ["src/**/__tests__/*"],
  "compilerOptions": {
    "composite": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

### 3. ESLint 配置 (.eslintrc.cjs)

```javascript
module.exports = {
  root: true,
  extends: [
    'plugin:vue/vue3-essential',
    'eslint:recommended',
    '@vue/eslint-config-typescript',
    '@vue/eslint-config-prettier/skip-formatting',
  ],
  parserOptions: {
    ecmaVersion: 'latest',
  },
}
```

### 4. Prettier 配置 (.prettierrc.json)

```json
{
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

### 5. Stylelint 配置 (stylelint.config.cjs)

```javascript
module.exports = {
  extends: [
    'stylelint-config-standard',
    'stylelint-config-recommended-vue',
    'stylelint-config-prettier',
  ],
  overrides: [
    {
      files: ['**/*.scss'],
      customSyntax: 'postcss-scss',
    },
    {
      files: ['**/*.vue'],
      customSyntax: 'postcss-html',
    },
  ],
}
```

## 🎨 主题定制

### Element Plus 主题变量 (src/styles/element-variables.scss)

```scss
:root {
  --el-color-primary: #409eff;
  --el-color-success: #67c23a;
  --el-color-warning: #e6a23c;
  --el-color-danger: #f56c6c;
  --el-color-info: #909399;
}
```

### 引入主题 (src/main.ts)

```typescript
import '@/styles/element-variables.scss'
import 'element-plus/theme-chalk/dark/css-vars.css'
import 'element-plus/theme-chalk/src/index.scss'
```

## 🔧 开发工具配置

### 1. VS Code 设置 (.vscode/settings.json)

- **自动保存**: 延迟 1 秒自动保存
- **格式化**: 保存时自动格式化
- **代码修复**: 保存时自动运行 ESLint 修复
- **导入整理**: 保存时自动整理导入语句

### 2. EditorConfig (.editorconfig)

- 统一缩进风格 (2 空格)
- 统一换行符 (LF)
- 统一字符编码 (UTF-8)

### 3. Git Hooks (.husky/)

- **commit-msg**: 检查提交信息格式
- **pre-commit**: 提交前自动格式化代码

## 📝 代码规范

### Git 提交规范

遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

```
<type>(<scope>): <subject>

[可选正文]
[可选 Footer]
```

常用类型：

- `feat`: 新功能
- `fix`: 修复 bug
- `docs`: 文档变更
- `style`: 代码格式
- `refactor`: 代码重构
- `perf`: 性能优化
- `test`: 测试相关
- `chore`: 构建工具

### 代码检查

```bash
# ESLint 检查
pnpm lint

# 格式化代码
pnpm format

# TypeScript 类型检查
pnpm type-check
```

## 🚀 部署

### 构建生产版本

```bash
pnpm build
```

构建产物位于 `dist/` 目录。

### 预览构建结果

```bash
pnpm preview
```

## 📚 推荐扩展

### VS Code 扩展

- **Vue Language Features (Volar)** - Vue 3 语言支持
- **ESLint** - JavaScript 代码检查
- **Prettier** - 代码格式化
- **Stylelint** - CSS/SCSS 代码检查
- **EditorConfig** - 编辑器配置
- **TypeScript** - TypeScript 支持
- **Auto Rename Tag** - 自动重命名标签
- **Path Intellisense** - 路径智能提示

## 🔄 更新维护

### 更新依赖

```bash
# 检查可更新的包
pnpm outdated

# 更新所有依赖
pnpm update

# 更新特定包
pnpm add package-name@latest
```

### 清理缓存

```bash
# 清理 pnpm 缓存
pnpm store prune

# 重新安装依赖
pnpm install --force
```

## 🐛 常见问题

### 1. crypto.hash is not a function

**原因**: Node.js 版本与某些依赖不兼容
**解决**: 升级 Node.js 到 20+ 版本

### 2. 样式文件编译错误

**原因**: SCSS 语法冲突
**解决**: 检查 vite.config.ts 中的 scss 配置

### 3. 自动导入不生效

**原因**: 插件配置问题
**解决**: 检查 vite.config.ts 中的 AutoImport 和 Components 配置

## 📞 技术支持

如遇到问题，请检查：

1. Node.js 版本是否符合要求
2. 依赖是否正确安装
3. 配置文件是否正确
4. 控制台错误信息

---

**最后更新**: 2024年12月
**版本**: 1.0.0
