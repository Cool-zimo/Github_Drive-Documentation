# 贡献指南

感谢你对 GitHub Drive 的贡献！本文档说明如何提交改进以及 CI/CD 自动审批流程。

## 快速开始

1. Fork 本仓库
2. 创建你的功能分支 (`git checkout -b feature/amazing-feature`)
3. 提交你的更改 (`git commit -m 'Add amazing feature'`)
4. **创建 `config.json` 配置文件**（必须）
5. 推送到分支 (`git push origin feature/amazing-feature`)
6. 开启 Pull Request

## config.json 配置文件（必须）

所有 Pull Request 必须在仓库根目录包含 `config.json` 文件，否则会被自动关闭。

### 模板

```json
{
  "author": "your-github-username",
  "name": "My Awesome Feature",
  "branch": "my-feature-branch",
  "description": "Describe what this version improves or adds",
  "version": "1.0.0",
  "contact": "your-email@example.com"
}
```

### 字段说明

| 字段 | 必须 | 说明 |
|------|------|------|
| `author` | ✅ | 你的 GitHub 用户名 |
| `name` | ✅ | 版本/功能名称 |
| `branch` | ✅ | 分支名（用于生成预览分支） |
| `description` | ❌ | 改进描述 |
| `version` | ❌ | 版本号 |
| `contact` | ❌ | 联系方式 |

## CI/CD 自动审批流程

当你提交 Pull Request 时，GitHub Actions 会自动执行以下操作：

### 1. 验证 config.json
- 检查 `config.json` 是否存在
- 验证必须字段（author、name、branch）
- **如果缺少 config.json，PR 会被自动关闭**

### 2. 创建预览分支
- 验证通过后，自动创建预览分支：`preview/{author}/{branch}`
- 你的代码会被推送到此分支

### 3. 自动评论
- 在 PR 下评论，告知预览分支名
- 提供测试方法和直接访问链接

## 如何测试他人的改进版本

### 方法一：应用内切换
1. 打开 GitHub Drive
2. 进入 **设置 → 版本切换**
3. 在列表中选择预览分支，或手动输入分支名
4. 点击"切换分支"，页面自动刷新加载新版本

### 方法二：URL 参数
直接访问：
```
https://cool-zimo.github.io/github_drive/?branch=preview/author/feature-name
```

### 恢复官方版本
1. 进入 **设置 → 版本切换**
2. 点击"恢复官方版"
3. 或清除 localStorage 中的 `gd_custom_branch`

## 注意事项

- 预览分支的代码从 `raw.githubusercontent.com` 加载，首次加载可能较慢
- 他人改进版本可能包含未经验证的代码，请谨慎使用
- 如果预览分支不存在或 Pages 未部署，页面可能无法正常加载
- 官方版本始终在 `main` 分支

## 代码规范

- 保持代码简洁、可读
- 遵循现有代码风格
- 添加必要的注释
- 测试你的更改后再提交

## 问题反馈

如果遇到问题，请在 GitHub 提交 Issue。
