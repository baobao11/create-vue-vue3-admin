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

| 类型     | 说明                                   |
| -------- | -------------------------------------- |
| feat     | 新增功能                               |
| fix      | 修复 bug                               |
| docs     | 文档变更                               |
| style    | 代码格式（不影响功能，如空格、分号等） |
| refactor | 代码重构（不包括 bug 修复、功能新增）  |
| perf     | 性能优化                               |
| test     | 增加/修改测试                          |
| chore    | 构建流程、工具等变动                   |
| revert   | 回滚提交                               |
| ci       | 持续集成相关                           |

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
