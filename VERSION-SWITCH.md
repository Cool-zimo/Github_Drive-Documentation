# 版本切换功能

GitHub Drive 支持加载他人改进的版本，通过预览分支机制实现。

## 功能概述

- 官方版本：`main` 分支，通过 GitHub Pages 部署
- 预览版本：`preview/{author}/{branch}` 分支，由 CI/CD 自动创建
- 用户可以在应用内切换到任意预览分支体验新功能

## 如何切换版本

### 1. 通过设置页面

1. 点击左下角 **设置**
2. 选择 **🔀 版本切换**
3. 在列表中点击可用的预览分支，或手动输入分支名
4. 点击 **切换分支**
5. 页面自动刷新，加载新版本

### 2. 通过 URL 参数

直接在 URL 后添加 `?branch=` 参数：

```
https://cool-zimo.github.io/github_drive/?branch=preview/username/feature-name
```

### 3. 恢复官方版本

- 在版本切换页面点击 **🏠 恢复官方版**
- 或在浏览器控制台执行：`localStorage.removeItem('gd_custom_branch')`

## 预览分支列表

版本切换页面会自动列出所有 `preview/` 开头的分支。这些分支由 CI/CD 在 Pull Request 时自动创建。

分支命名格式：
```
preview/{author}/{sanitized-branch-name}
```

示例：
- `preview/cool-zimo/dark-mode`
- `preview/developer123/new-feature`

## 技术实现

### 资源加载

当检测到自定义分支时：
1. 从 `localStorage` 读取 `gd_custom_branch`
2. 或从 URL 参数 `?branch=` 读取
3. 动态从 `raw.githubusercontent.com/Cool-zimo/github_drive/{branch}/` 加载 CSS 和 JS

### 注意事项

- `raw.githubusercontent.com` 在国内可能访问较慢
- 预览分支不会触发 GitHub Pages 部署，资源直接从 GitHub 加载
- 如果分支不存在，页面会加载失败
- 切换分支后，所有本地数据（token、配置等）保持不变

## 开发者指南

### 提交改进

1. Fork 仓库
2. 创建功能分支
3. 添加 `config.json`（必须）
4. 提交 Pull Request
5. CI/CD 自动创建预览分支

详见 [CONTRIBUTING.md](./CONTRIBUTING.md)

### config.json 示例

```json
{
  "author": "your-username",
  "name": "Dark Mode Theme",
  "branch": "dark-mode",
  "description": "Add dark mode support",
  "version": "1.0.0"
}
```

## 常见问题

**Q: 切换分支后页面空白？**
A: 可能是预览分支不存在或代码有错误。请恢复官方版本，或检查分支名是否正确。

**Q: 切换分支后我的文件还在吗？**
A: 文件存储在 GitHub 仓库中，与应用版本无关。切换分支不会影响你的文件。

**Q: 预览版本安全吗？**
A: 预览版本是第三方提交的代码，可能包含未经验证的更改。请谨慎使用，官方版本始终在 main 分支。

**Q: 如何知道哪些预览分支可用？**
A: 在版本切换页面会自动列出所有 preview/ 开头的分支，也可以访问 GitHub 仓库的 Branches 页面查看。
