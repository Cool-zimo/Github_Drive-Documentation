# GitHub Drive 文档

基于 GitHub API 的虚拟文件系统 - 把多个 GitHub 仓库变成一个统一的云端硬盘。

## 📚 文档目录

### 用户指南
- [快速开始](#快速开始)
- [功能介绍](#功能介绍)
- [常见问题](#常见问题)

### 开发者文档
- [插件开发指南](#插件开发指南)
- [API 参考](#api-参考)
- [后端服务](#后端服务)

## 🚀 快速开始

1. 生成 GitHub Personal Access Token（需要 repo 和 workflow 权限）
2. 打开 [GitHub Drive](https://cool-zimo.github.io/github_drive/)
3. 输入 Token，点击"进入 Drive"
4. 开始使用！

## ✨ 功能介绍

- **文件管理**：上传、下载、删除、移动、重命名文件和文件夹
- **大文件支持**：自动分片上传，支持任意大小文件
- **多仓库存储**：自动创建和管理多个存储仓库，突破单仓库容量限制
- **文件分享**：一键生成分享链接，支持二维码
- **插件系统**：丰富的插件生态，支持游戏、工具等
- **多账号管理**：支持多个 GitHub 账号切换
- **后端服务**：可选的本地后端，突破 CORS 限制

## 🔌 插件开发指南

### 插件格式

插件是一个独立的 HTML 文件，可以通过 GitHub Drive 提供的 API 与主程序交互。

### 插件清单

在 `plugins.json` 中注册你的插件：

```json
{
  "id": "your-plugin-id",
  "name": "插件名称",
  "description": "插件描述",
  "author": "作者",
  "version": "1.0.0",
  "icon": "🔧",
  "file": "plugins/your-plugin.html",
  "type": "plugin"
}
```

### 可用 API

插件可以通过 `window.parent.postMessage` 与主程序交互：

- `getToken` - 获取当前用户的 GitHub Token
- `getUser` - 获取当前用户信息
- `readFile` - 读取 Drive 中的文件
- `writeFile` - 写入文件到 Drive
- `listFiles` - 列出文件

## 🖥️ 后端服务

部分插件（如 B 站视频下载器）需要后端服务才能运行。

### 下载后端

在 GitHub Drive 的插件广场中，点击"后端服务"卡片的"加速下载"按钮，选择对应系统的可执行文件下载。

### 运行后端

下载后双击运行，后端会在 `http://localhost:8787` 启动，GitHub Drive 会自动连接。

### 后端 API

- `GET /api/request` - 通用网络请求代理
- `POST /api/exec` - 执行命令（需用户确认）
- `GET /api/drive/read` - 读取 Drive 文件
- `POST /api/drive/write` - 写入 Drive 文件

## ❓ 常见问题

### Q: 上传大文件失败怎么办？
A: 检查 Token 是否有 repo 权限，确保网络连接稳定。大文件会自动分片上传，失败会自动清理已上传的分片。

### Q: 如何切换账号？
A: 点击左下角的用户头像，选择"切换账号"，可以添加和管理多个 GitHub 账号。

### Q: 分享的文件多久生效？
A: GitHub Pages 部署需要 1-5 分钟，分享后请稍等片刻再访问。

## 📝 许可证

MIT License


## 文档

- [贡献指南](./CONTRIBUTING.md) - 如何提交改进和 CI/CD 流程
- [版本切换](./VERSION-SWITCH.md) - 如何体验他人改进的版本
