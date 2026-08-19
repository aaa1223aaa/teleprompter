# 🎤 跟嘴走 · 语音跟随提词器

一个基于语音识别的智能提词器：你说在哪里，高亮就跟到哪里。

## ✨ 功能特点

- **语音跟随**：实时识别你的语音，自动高亮当前阅读位置
- **精准匹配**：支持模糊匹配，轻微漏字、重复、停顿都不会乱跳
- **实时语速**：右上角实时显示当前语速（字/分钟）
- **朗读结算**：读完全文后弹出数据报告，包含语速、精准度等统计
- **响应式设计**：支持手机和电脑浏览器
- **隐私安全**：所有处理都在本地浏览器完成，不上传任何数据

## 🚀 快速开始

### 1. 启动 HTTPS 服务器

```bash
cd teleprompter
node https-server.js
```

### 2. 打开页面

- **电脑**：https://localhost:8080/teleprompter-standalone.html
- **手机**：https://你的局域网IP:8080/teleprompter-standalone.html

> ⚠️ 首次打开会提示「不安全」，点击「高级」→「继续前往」即可。

## 📱 浏览器兼容

| 浏览器 | 支持情况 |
|--------|----------|
| Safari (iOS/macOS) | ✅ 完美支持 |
| Chrome (Android/macOS/Windows) | ✅ 支持（需要网络） |
| Edge | ✅ 支持 |
| Firefox | ❌ 不支持 Web Speech API |

## 🛠️ 技术栈

- **前端**：纯 HTML/CSS/JavaScript，无框架依赖
- **语音识别**：Web Speech API（Safari 使用本地引擎，Chrome 使用 Google 云端）
- **服务器**：Node.js HTTPS（用于局域网访问和麦克风权限）

## 📁 项目结构

```
teleprompter/
├── teleprompter-standalone.html   # 提词器主页面
├── https-server.js                # HTTPS 服务器
├── cert.pem                       # SSL 证书（自签名）
├── key.pem                        # SSL 私钥
├── .gitignore
└── README.md
```

## 📄 License

MIT
