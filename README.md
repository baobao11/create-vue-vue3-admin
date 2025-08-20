# Vue3 Admin 脚手架

一个基于 Vue 3 + TypeScript + Vite 的现代化管理后台脚手架，集成了完整的开发工具链和最佳实践。

## ✨ 特性

- 🚀 **Vue 3** - 使用 Composition API 和 `<script setup>`
- 📦 **TypeScript** - 完整的类型支持
- ⚡ **Vite** - 极速的开发体验
- 🎨 **Element Plus** - 自动按需导入的 UI 组件库
- 📝 **代码规范** - ESLint + Prettier + Stylelint
- 🔧 **Git 规范** - Commitlint + Husky
- 🎯 **自动导入** - Vue、Vue Router、Element Plus 组件
- 🌙 **主题定制** - 支持 Element Plus 主题变量
- 💾 **自动保存** - VS Code 自动保存和格式化

## 🚀 快速开始

### 环境要求

- Node.js >= 18.0.0 (推荐 20+)
- pnpm >= 8.0.0

### 安装

```bash
# 克隆项目
git clone <repository-url>
cd vue3-admin

# 安装依赖
pnpm install

# 启动开发服务器
pnpm dev
```

### 构建

```bash
# 构建生产版本
pnpm build

# 预览构建结果
pnpm preview
```

## 📁 项目结构

```
vue3-admin/
├── .vscode/                    # VS Code 配置
├── .husky/                     # Git hooks
├── docs/                       # 项目文档
├── src/                        # 源代码
│   ├── assets/                 # 静态资源
│   ├── components/             # 公共组件
│   ├── router/                 # 路由配置
│   ├── stores/                 # 状态管理
│   ├── styles/                 # 样式文件
│   ├── views/                  # 页面组件
│   ├── App.vue                 # 根组件
│   └── main.ts                 # 入口文件
├── .editorconfig               # 编辑器配置
├── .eslint.config.ts              # ESLint 配置
├── .prettierrc.json           # Prettier 配置
├── commitlint.config.js        # Commitlint 配置
├── stylelint.config.cjs        # Stylelint 配置
├── tsconfig.app.json              # TypeScript 配置
├── vite.config.ts             # Vite 配置
└── package.json               # 项目配置
```

## 🛠 技术栈

### 核心框架

- Vue 3.5.18
- TypeScript 5.8.3
- Vite 7.0.6
- Vue Router 4.5.1
- Pinia 3.0.3

### UI 组件库

- Element Plus 2.10.4 (自动按需导入)

### 开发工具

- ESLint 9.32.0
- Prettier 3.6.2
- Stylelint 16.22.0
- Husky 9.1.7
- lint-staged 16.1.2

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

## 🎨 主题定制

项目支持 Element Plus 主题定制，配置文件位于 `src/styles/element-variables.scss`：

```scss
:root {
  --el-color-primary: #409eff;
  --el-color-success: #67c23a;
  --el-color-warning: #e6a23c;
  --el-color-danger: #f56c6c;
  --el-color-info: #909399;
}
```

## 🔧 开发工具

### VS Code 扩展

项目已配置以下 VS Code 扩展：

- Vue Language Features (Volar)
- ESLint
- Prettier
- Stylelint
- EditorConfig
- TypeScript
- Auto Rename Tag
- Path Intellisense

### 自动保存和格式化

- 文件自动保存 (延迟 1 秒)
- 保存时自动格式化
- 保存时自动运行 ESLint 修复
- 保存时自动整理导入语句

## 📚 文档

- [脚手架搭建指南](./docs/scaffold-guide.md) - 详细的技术栈和配置说明
- [Git 提交规范](./docs/commit-convention.md) - 代码提交规范

## 🐛 常见问题

### 1. crypto.hash is not a function

**解决**: 升级 Node.js 到 20+ 版本

### 2. 样式文件编译错误

**解决**: 检查 vite.config.ts 中的 scss 配置

### 3. 自动导入不生效

**解决**: 检查 vite.config.ts 中的 AutoImport 和 Components 配置

## 📄 许可证

[MIT License](./LICENSE)

---

**最后更新**: 2024年12月
**版本**: 1.0.0
