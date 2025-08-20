# Vue3 Admin 项目搭建详细教程

本教程将带你从零开始，一步一步搭建一个完整的 Vue3 Admin 项目，包含所有最佳实践和工具链配置。

## 📋 目录

1. [环境准备](#环境准备)
2. [项目初始化](#项目初始化)
3. [基础配置](#基础配置)
4. [代码规范集成](#代码规范集成)
5. [Git 提交规范](#git-提交规范)
6. [UI 组件库集成](#ui-组件库集成)
7. [主题定制](#主题定制)
8. [开发工具配置](#开发工具配置)
9. [文档生成](#文档生成)
10. [项目测试](#项目测试)

---

## 1. 环境准备

### 1.1 安装 Node.js

确保你的 Node.js 版本 >= 18.0.0（推荐 20+）：

```bash
# 检查 Node.js 版本
node --version

# 如果版本过低，请升级到最新版本
# 推荐使用 nvm 管理 Node.js 版本
```

### 1.2 安装 pnpm

```bash
# 安装 pnpm
npm install -g pnpm

# 检查 pnpm 版本
pnpm --version
```

### 1.3 准备开发环境

确保你有一个代码编辑器（推荐 VS Code），并安装以下扩展：

- Vue Language Features (Volar)
- TypeScript
- ESLint
- Prettier
- EditorConfig

---

## 2. 项目初始化

### 2.1 创建 Vue 项目

```bash
# 使用 create-vue 创建项目
pnpm create vue@latest vue3-admin

# 选择以下选项：
# ✓ Add TypeScript? Yes
# ✓ Add JSX Support? Yes
# ✓ Add Vue Router? Yes
# ✓ Add Pinia? Yes
# ✓ Add Vitest? No
# ✓ Add End-to-End Testing? No
# ✓ Add ESLint? Yes
# ✓ Add Prettier? Yes

# 进入项目目录
cd vue3-admin
```

### 2.2 安装依赖

```bash
# 安装项目依赖
pnpm install
```

### 2.3 测试项目

```bash
# 启动开发服务器
pnpm dev

# 访问 http://localhost:5173 确认项目正常运行
```

---

## 3. 基础配置

### 3.1 配置 TypeScript

编辑 `tsconfig.app.json`：

```json
{
  "extends": "@vue/tsconfig/tsconfig.dom.json",
  "include": ["env.d.ts", "src/**/*", "src/**/*.vue"],
  "exclude": ["src/**/__tests__/*"],
  "compilerOptions": {
    "tsBuildInfoFile": "./node_modules/.tmp/tsconfig.app.tsbuildinfo",
    "composite": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

### 3.2 配置 Vite

编辑 `vite.config.ts`：

```typescript
import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueJsx from '@vitejs/plugin-vue-jsx'
import vueDevTools from 'vite-plugin-vue-devtools'

export default defineConfig({
  plugins: [vue(), vueJsx(), vueDevTools()],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url)),
    },
  },
})
```

### 3.3 配置 ESLint

编辑 `eslint.config.ts`：

```javascript
import { globalIgnores } from 'eslint/config'
import { defineConfigWithVueTs, vueTsConfigs } from '@vue/eslint-config-typescript'
import pluginVue from 'eslint-plugin-vue'
import skipFormatting from '@vue/eslint-config-prettier/skip-formatting'

// To allow more languages other than `ts` in `.vue` files, uncomment the following lines:
// import { configureVueProject } from '@vue/eslint-config-typescript'
// configureVueProject({ scriptLangs: ['ts', 'tsx'] })
// More info at https://github.com/vuejs/eslint-config-typescript/#advanced-setup

export default defineConfigWithVueTs(
  {
    name: 'app/files-to-lint',
    files: ['**/*.{ts,mts,tsx,vue}'],
  },

  globalIgnores(['**/dist/**', '**/dist-ssr/**', '**/coverage/**']),

  pluginVue.configs['flat/essential'],
  vueTsConfigs.recommended,
  skipFormatting,
)
```

### 3.4 配置 Prettier

编辑 `.prettierrc.json`：

```json
{
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

---

## 4. 代码规范集成

### 4.1 安装 Stylelint

```bash
# 安装 Stylelint 相关依赖（强烈建议使用 15.x 版本，避免 16.x 规则不兼容报错）
pnpm add -D stylelint@15.11.0 stylelint-config-standard@34.0.0 stylelint-config-prettier@9.0.5 stylelint-config-recommended-vue@1.4.0 stylelint-scss@4.6.0
```

> ⚠️ 注意：请务必安装 stylelint 15.x 及对应版本的依赖，避免 16.x 及以上版本导致的“Unknown rule”报错。
>
> 推荐命令如上，或参考：
>
> ```bash
> pnpm add -D stylelint@15.11.0 stylelint-config-standard@34.0.0 stylelint-config-prettier@9.0.5 stylelint-config-recommended-vue@1.4.0 stylelint-scss@4.6.0
> ```

### 4.2 配置 Stylelint

创建 `.stylelintrc.json`：

```javascript
{
  "$schema": "https://json.schemastore.org/stylelintrc",
  "extends": [
    "stylelint-config-standard",
    "stylelint-config-recommended-vue",
    "stylelint-config-prettier"
  ],
  "plugins": ["stylelint-order"],
  "rules": {
    "order/properties-order": [
      "position",
      "top",
      "right",
      "bottom",
      "left",
      "z-index",
      "display",
      "float",
      "width",
      "height",
      "max-width",
      "max-height",
      "min-width",
      "min-height",
      "padding",
      "padding-top",
      "padding-right",
      "padding-bottom",
      "padding-left",
      "margin",
      "margin-top",
      "margin-right",
      "margin-bottom",
      "margin-left",
      "border",
      "border-top",
      "border-right",
      "border-bottom",
      "border-left",
      "border-radius",
      "background",
      "background-color",
      "background-image",
      "background-repeat",
      "background-position",
      "background-size",
      "color",
      "font",
      "font-family",
      "font-size",
      "font-weight",
      "line-height",
      "text-align",
      "text-decoration",
      "text-transform",
      "cursor",
      "opacity",
      "transition",
      "transform",
      "animation"
    ],
    "selector-class-pattern": null,
    "keyframes-name-pattern": null,
    "custom-property-pattern": null,
    "no-descending-specificity": null,
    "alpha-value-notation": "percentage",
    "color-function-notation": "modern",
    "selector-pseudo-class-no-unknown": [
      true,
      {
        "ignorePseudoClasses": ["global", "deep"]
      }
    ],
    "selector-pseudo-element-no-unknown": [
      true,
      {
        "ignorePseudoElements": ["v-deep", "v-global", "v-slotted"]
      }
    ],
    "no-duplicate-selectors": null,
    "declaration-block-trailing-semicolon": null,
    "declaration-colon-space-after": null,
    "declaration-colon-space-before": null,
    "declaration-block-semicolon-newline-after": null,
    "declaration-block-semicolon-newline-before": null,
    "declaration-block-semicolon-space-after": null,
    "declaration-block-semicolon-space-before": null,
    "block-opening-brace-newline-after": null,
    "block-opening-brace-newline-before": null,
    "block-opening-brace-space-after": null,
    "block-opening-brace-space-before": null,
    "block-closing-brace-newline-after": null,
    "block-closing-brace-newline-before": null,
    "block-closing-brace-space-after": null,
    "block-closing-brace-space-before": null,
    "block-closing-brace-empty-line-before": null,
    "function-comma-newline-after": null,
    "function-comma-newline-before": null,
    "function-comma-space-after": null,
    "function-comma-space-before": null,
    "function-parentheses-newline-inside": null,
    "function-parentheses-space-inside": null,
    "value-list-comma-newline-after": null,
    "value-list-comma-newline-before": null,
    "value-list-comma-space-after": null,
    "value-list-comma-space-before": null,
    "selector-list-comma-newline-after": null,
    "selector-list-comma-newline-before": null,
    "selector-list-comma-space-after": null,
    "selector-list-comma-space-before": null,
    "media-feature-colon-space-after": null,
    "media-feature-colon-space-before": null,
    "media-feature-parentheses-space-inside": null,
    "media-query-list-comma-newline-after": null,
    "media-query-list-comma-newline-before": null,
    "media-query-list-comma-space-after": null,
    "media-query-list-comma-space-before": null,
    "selector-attribute-brackets-space-inside": null,
    "selector-attribute-operator-space-after": null,
    "selector-attribute-operator-space-before": null,
    "selector-combinator-space-after": null,
    "selector-combinator-space-before": null,
    "selector-descendant-combinator-no-non-space": null,
    "selector-pseudo-class-parentheses-space-inside": null,
    "at-rule-name-case": null,
    "at-rule-name-newline-after": null,
    "at-rule-name-space-after": null,
    "at-rule-semicolon-newline-after": null,
    "at-rule-semicolon-space-before": null,
    "color-hex-case": null,
    "declaration-bang-space-after": null,
    "declaration-bang-space-before": null,
    "function-max-empty-lines": null,
    "max-empty-lines": null,
    "max-line-length": null,
    "media-feature-name-case": null,
    "no-empty-first-line": null,
    "no-eol-whitespace": null,
    "no-extra-semicolons": null,
    "no-missing-end-of-source-newline": null,
    "number-leading-zero": null,
    "number-no-trailing-zeros": null,
    "property-case": null,
    "selector-max-empty-lines": null,
    "selector-pseudo-class-case": null,
    "selector-pseudo-element-case": null,
    "string-quotes": null,
    "unicode-bom": null,
    "unit-case": null,
    "value-list-max-empty-lines": null,
    "indentation": null,
    "linebreaks": null
  },
  "overrides": [
    {
      "files": ["**/*.vue"],
      "customSyntax": "postcss-html"
    }
  ]
}

```

### 4.3 安装 lint-staged

```bash
# 安装 lint-staged
pnpm add -D lint-staged
```

### 4.4 配置 lint-staged

编辑 `package.json`，添加 lint-staged 配置：

```json
{
  "lint-staged": {
    "*.{js,ts,vue}": ["eslint --fix", "prettier --write"],
    "*.{css,scss,vue}": ["stylelint --fix"],
    "*.{json,md}": ["prettier --write"]
  }
}
```

---

## 5. Git 提交规范

### 5.1 安装 Husky 和 Commitlint

```bash
# 安装 Husky 和 Commitlint
pnpm add -D husky @commitlint/cli @commitlint/config-conventional
```

### 5.2 初始化 Husky

```bash
# 初始化 Husky
pnpm dlx husky init

# 添加 prepare 脚本到 package.json
```

编辑 `package.json`，在 scripts 中添加：

```json
{
  "scripts": {
    "prepare": "husky install"
  }
}
```

### 5.3 配置 Git Hooks

```bash
# Husky的add命令已被弃用， 手动创建钩子文件，根目录创建.husky文件，.husky文件下创建commit-msg和lint-staged文件
# 添加 commit-msg hook
 .husky/commit-msg文件：  "npx --no-install commitlint --edit $1"

# 添加 pre-commit hook
 .husky/pre-commit文件： "npx --no-install lint-staged"

```

### 5.4 配置 Commitlint

创建 `commitlint.config.js`：

```javascript
module.exports = {
  extends: ['@commitlint/config-conventional'],
}
```

### 5.5 初始化 Git 仓库

```bash
# 初始化 Git 仓库
git init

# 添加所有文件
git add .

# 提交初始代码
git commit -m "feat: 初始化 Vue3 Admin 项目"
```

---

## 6. UI 组件库集成

### 6.1 安装 Element Plus

```bash
# 安装 Element Plus
pnpm add element-plus

# 安装自动导入插件
pnpm add -D unplugin-auto-import unplugin-vue-components
```

### 6.2 配置自动导入

编辑 `vite.config.ts`：

```typescript
import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueJsx from '@vitejs/plugin-vue-jsx'
import vueDevTools from 'vite-plugin-vue-devtools'
import AutoImport from 'unplugin-auto-import/vite'
import Components from 'unplugin-vue-components/vite'
import { ElementPlusResolver } from 'unplugin-vue-components/resolvers'

export default defineConfig({
  plugins: [
    vue(),
    vueJsx(),
    vueDevTools(),
    AutoImport({
      imports: ['vue', 'vue-router'],
      resolvers: [ElementPlusResolver()],
      dts: 'src/auto-imports.d.ts',
    }),
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

### 6.3 测试自动导入

创建一个测试组件 `src/components/TestElement.vue`：

```vue
<template>
  <div>
    <el-button type="primary">测试按钮</el-button>
    <el-input v-model="inputValue" placeholder="测试输入框" />
  </div>
</template>

<script setup lang="ts">
const inputValue = ref('')
</script>
```

---

## 7. 主题定制

### 7.1 创建样式目录

```bash
# 创建样式目录
mkdir -p src/styles
```

### 7.2 创建主题变量文件

创建 `src/styles/element-variables.scss`：

```scss
:root {
  --el-color-primary: #409eff;
  --el-color-success: #67c23a;
  --el-color-warning: #e6a23c;
  --el-color-danger: #f56c6c;
  --el-color-info: #909399;
}
```

### 7.3 引入主题样式

编辑 `src/main.ts`：

```typescript
import './assets/main.css'

import { createApp } from 'vue'
import { createPinia } from 'pinia'

import App from './App.vue'
import router from './router'

// 引入 Element Plus 主题
import '@/styles/element-variables.scss'
import 'element-plus/theme-chalk/dark/css-vars.css'
import 'element-plus/theme-chalk/src/index.scss'

const app = createApp(App)

app.use(createPinia())
app.use(router)

app.mount('#app')
```

---

## 8. 开发工具配置

### 8.1 创建 VS Code 配置

创建 `.vscode/settings.json`：

```json
{
  "explorer.fileNesting.enabled": true,
  "explorer.fileNesting.patterns": {
    "tsconfig.json": "tsconfig.*.json, env.d.ts",
    "vite.config.*": "jsconfig*, vitest.config.*, cypress.config.*, playwright.config.*",
    "package.json": "package-lock.json, pnpm*, .yarnrc*, yarn*, .eslint*, eslint*, .oxlint*, oxlint*, .prettier*, prettier*, .editorconfig"
  },
  "files.autoSave": "afterDelay",
  "files.autoSaveDelay": 1000,
  "editor.formatOnSave": true,
  "editor.formatOnPaste": true,
  "editor.formatOnType": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll": "explicit",
    "source.fixAll.eslint": "explicit",
    "source.organizeImports": "explicit"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[vue]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[css]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[scss]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[markdown]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "eslint.validate": ["javascript", "javascriptreact", "typescript", "typescriptreact", "vue"],
  "eslint.autoFixOnSave": true,
  "stylelint.validate": ["css", "scss", "vue"],
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.detectIndentation": false,
  "editor.rulers": [80, 120],
  "editor.wordWrap": "on",
  "editor.minimap.enabled": false,
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": true,
  "editor.suggestSelection": "first",
  "editor.acceptSuggestionOnCommitCharacter": false,
  "editor.acceptSuggestionOnEnter": "on"
}
```

### 8.2 创建扩展推荐

创建 `.vscode/extensions.json`：

```json
{
  "recommendations": [
    "Vue.volar",
    "dbaeumer.vscode-eslint",
    "EditorConfig.EditorConfig",
    "esbenp.prettier-vscode",
    "stylelint.vscode-stylelint",
    "bradlc.vscode-tailwindcss",
    "ms-vscode.vscode-typescript-next",
    "formulahendry.auto-rename-tag",
    "christian-kohler.path-intellisense",
    "ms-vscode.vscode-json"
  ]
}
```

### 8.3 创建 EditorConfig

创建 `.editorconfig`：

```ini
# EditorConfig is awesome: https://EditorConfig.org

# top-most EditorConfig file
root = true

# Unix-style newlines with a newline ending every file
[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
indent_style = space
indent_size = 2

# Markdown files
[*.md]
trim_trailing_whitespace = false

# TypeScript and JavaScript files
[*.{ts,tsx,js,jsx}]
indent_size = 2

# Vue files
[*.vue]
indent_size = 2

# JSON files
[*.json]
indent_size = 2

# CSS, SCSS files
[*.{css,scss}]
indent_size = 2

# HTML files
[*.html]
indent_size = 2

# YAML files
[*.{yml,yaml}]
indent_size = 2
```

---

## 9. 文档生成

### 9.1 创建文档目录

```bash
# 创建文档目录
mkdir -p docs
```

### 9.2 创建 Git 提交规范文档

创建 `docs/commit-convention.md`：

```markdown
# Git 提交规范（Conventional Commits）

为了保证提交记录的清晰和可读性，项目采用 [Conventional Commits](https://www.conventionalcommits.org/zh-hans/v1.0.0/) 规范。

## 提交格式
```

<type>(<scope>): <subject>

[可选正文]
[可选 Footer]

```

- `type`：提交类型（必填）
- `scope`：影响范围（可选）
- `subject`：简要描述（必填，建议不超过50字）
- `body`：详细描述（可选）
- `footer`：关联 issue 或 BREAKING CHANGE（可选）

## 常用 type 类型

| 类型     | 说明           |
|----------|----------------|
| feat     | 新增功能       |
| fix      | 修复 bug       |
| docs     | 文档变更       |
| style    | 代码格式（不影响功能，如空格、分号等）|
| refactor | 代码重构（不包括 bug 修复、功能新增）|
| perf     | 性能优化       |
| test     | 增加/修改测试  |
| chore    | 构建流程、工具等变动 |
| revert   | 回滚提交       |
| ci       | 持续集成相关   |

## 示例

```

feat(login): 新增用户登录功能

fix: 修复页面加载闪烁问题

docs: 更新 README 使用说明

style: 调整代码缩进为 2 空格

refactor: 优化数据处理逻辑

chore: 升级依赖包

revert: revert: feat(login): 新增用户登录功能

```

## 说明
- `subject` 以动词开头，首字母小写，结尾不加句号。
- 如有 `BREAKING CHANGE` 或 issue 关联，请在 Footer 说明。
- 所有提交信息会在 commit 时自动校验，不符合规范将无法提交。
```

### 9.3 创建脚手架搭建指南

创建 `docs/scaffold-guide.md`（内容见之前的详细文档）

### 9.4 更新 README.md

更新项目根目录的 `README.md`（内容见之前的快速入门指南）

---

## 10. 项目测试

### 10.1 测试开发服务器

```bash
# 启动开发服务器
pnpm dev

# 访问 http://localhost:5173 确认项目正常运行
```

### 10.2 测试代码检查

```bash
# 测试 ESLint
pnpm lint

# 测试 TypeScript 类型检查
pnpm type-check

# 测试格式化
pnpm format
```

### 10.3 测试 Git 提交规范

```bash
# 尝试提交不符合规范的代码
git add .
git commit -m "test commit"

# 应该被拒绝，然后使用正确的格式
git commit -m "feat: 初始化项目配置"
```

### 10.4 测试自动导入

在 `src/views/HomeView.vue` 中添加 Element Plus 组件：

```vue
<template>
  <div class="home">
    <el-card>
      <template #header>
        <div class="card-header">
          <span>欢迎使用 Vue3 Admin</span>
        </div>
      </template>
      <el-button type="primary" @click="handleClick">点击测试</el-button>
    </el-card>
  </div>
</template>

<script setup lang="ts">
import { ElMessage } from 'element-plus'

const handleClick = () => {
  ElMessage.success('自动导入测试成功！')
}
</script>

<style scoped>
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>
```

### 10.5 测试构建

```bash
# 构建生产版本
pnpm build

# 预览构建结果
pnpm preview
```

---

## 🎉 完成！

恭喜！你已经成功搭建了一个完整的 Vue3 Admin 项目，包含：

✅ **Vue 3 + TypeScript + Vite** - 现代化技术栈  
✅ **Element Plus** - UI 组件库（自动按需导入）  
✅ **代码规范** - ESLint + Prettier + Stylelint  
✅ **Git 规范** - Commitlint + Husky  
✅ **自动保存** - VS Code 自动保存和格式化  
✅ **主题定制** - Element Plus 主题变量  
✅ **完整文档** - 项目文档和搭建指南

## 📚 下一步

1. **开始开发** - 根据业务需求开发具体功能
2. **添加路由** - 配置页面路由
3. **状态管理** - 使用 Pinia 管理状态
4. **API 集成** - 集成后端 API
5. **部署配置** - 配置生产环境部署

## 🔧 常用命令

```bash
# 开发
pnpm dev

# 构建
pnpm build

# 代码检查
pnpm lint

# 格式化
pnpm format

# 类型检查
pnpm type-check

# 预览构建
pnpm preview
```

---

**教程版本**: 1.0.0  
**最后更新**: 2024年12月
