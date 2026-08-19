# 🎤 跟嘴走 · 语音跟随提词器

一个基于语音识别的智能提词器：你说在哪里，高亮就跟到哪里。

![preview](https://img.shields.io/badge/平台-macOS%20%7C%20iOS%20%7C%20Android-blue) ![license](https://img.shields.io/badge/License-MIT-green)

## ✨ 功能特点

- 🎙️ **语音跟随**：实时识别你的语音，自动高亮当前阅读位置
- 🎯 **精准匹配**：支持模糊匹配，轻微漏字、重复、停顿都不会乱跳
- 📊 **实时语速**：右上角实时显示当前语速（字/分钟）
- 📋 **朗读结算**：读完全文后弹出数据报告，包含语速、精准度、覆盖率等统计
- 📱 **响应式设计**：支持手机和电脑浏览器
- 🔒 **隐私安全**：所有处理都在本地浏览器完成，不上传任何数据

## 🚀 快速开始

### 前置要求

- [Node.js](https://nodejs.org/)（v16 或更高版本）
- macOS / Linux / Windows 均可

### 1. 克隆项目

```bash
git clone https://github.com/aaa1223aaa/teleprompter.git
cd teleprompter
```

### 2. 生成 SSL 证书

手机浏览器（Safari / Chrome）要求 HTTPS 才能使用麦克风，需要先生成自签名证书：

```bash
# 获取你的局域网 IP（macOS）
IP=$(ipconfig getifaddr en0 || ipconfig getifaddr en1)
echo "你的局域网 IP: $IP"

# 生成证书（把下面的 IP 替换成你自己的）
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes \
  -subj "/CN=$IP" \
  -addext "subjectAltName=IP:$IP,IP:127.0.0.1,DNS:localhost"
```

### 3. 启动服务器

```bash
node https-server.js
```

看到以下输出说明启动成功：

```
HTTPS Server running on https://0.0.0.0:8080
```

### 4. 打开页面

| 设备 | 地址 |
|------|------|
| 🖥️ 电脑 | https://localhost:8080/teleprompter-standalone.html |
| 📱 手机 | https://你的局域网IP:8080/teleprompter-standalone.html |

> ⚠️ 首次打开会提示「不安全」，这是自签名证书的正常提示。点击 **「高级」→「继续前往」** 即可。

### 快捷启动（macOS）

```bash
# 一行命令搞定
cd teleprompter && IP=$(ipconfig getifaddr en0) && openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes -subj "/CN=$IP" -addext "subjectAltName=IP:$IP,IP:127.0.0.1,DNS:localhost" 2>/dev/null && node https-server.js
```

## 📱 使用方法

1. **粘贴文案**：在下方「文案」标签页中输入或粘贴你的口播稿
2. **开始跟读**：点击「开始跟读」按钮或按 `Space` 键
3. **允许麦克风**：浏览器会弹出麦克风权限请求，点击「允许」
4. **开始朗读**：对着麦克风说话，提词器会自动高亮你正在读的位置
5. **查看报告**：读完全文后会自动弹出朗读数据报告

### 快捷键

| 快捷键 | 功能 |
|--------|------|
| `Space` | 开始 / 暂停识别 |
| `←` | 向前回退一句 |
| `→` | 向后跳一句 |
| `F` | 全屏模式 |
| `Esc` | 退出全屏 |

## 📱 浏览器兼容

| 浏览器 | 支持情况 | 说明 |
|--------|----------|------|
| Safari (iOS / macOS) | ✅ 完美支持 | 使用苹果本地引擎，无需联网 |
| Chrome (Android / macOS / Windows) | ✅ 支持 | 使用 Google 云端识别，需要网络 |
| Edge | ✅ 支持 | 同 Chrome |
| Firefox | ❌ 不支持 | 不支持 Web Speech API |

> 💡 **推荐使用 Safari**，识别效果最好且完全离线。

## 🛠️ 技术栈

- **前端**：纯 HTML / CSS / JavaScript，零框架依赖
- **语音识别**：[Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API)
- **服务器**：Node.js 原生 HTTPS 模块

## 📁 项目结构

```
teleprompter/
├── teleprompter-standalone.html   # 提词器主页面（单文件，包含全部前端逻辑）
├── https-server.js                # Node.js HTTPS 静态文件服务器
├── cert.pem                       # SSL 证书（自签名，需自己生成）
├── key.pem                        # SSL 私钥（需自己生成）
├── .gitignore                     # 忽略证书和 node_modules
└── README.md                      # 项目说明
```

## ❓ 常见问题

**Q: 手机打开提示「无法连接」？**
A: 确保手机和电脑连接的是同一个 WiFi，且电脑防火墙允许 8080 端口。

**Q: Chrome 一直显示「正在重连」？**
A: Chrome 的语音识别依赖 Google 服务器，需要稳定的网络连接。建议改用 Safari。

**Q: 识别不准确怎么办？**
A: 在「跟随」标签页中调高灵敏度（选「灵敏」模式），可以更好地处理口误和跳词。

**Q: 证书过期了怎么办？**
A: 重新运行证书生成命令即可，证书有效期 365 天。

## 📄 License

[MIT](LICENSE)
