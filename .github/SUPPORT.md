# 《散页》（Loose Leaf）支持与帮助指南

> **Support & Help Guidelines · 宁静翻阅，答疑解惑**

欢迎查阅《散页》（Loose Leaf）支持中心。在使用本项目的单二进制服务端、Web 展厅、macOS 桌面工作台或 Android 随行端时，若遇到任何配置、配对或使用疑问，可按照以下索引寻求帮助。

---

## 一、权威文档专著地图

在提交咨询或报告问题前，请优先阅读对应专著文档，大多数常见疑问均在其中详细解答：

- **全平台生态架构与统筹蓝图**：[`docs/ecosystem.md`](https://github.com/Losse-Leaf/docs/blob/main/ecosystem.md)  
  了解四端协同边界、跨端设计语言映射、离线优先发件箱机制与演进路线。
- **后端中枢开发与部署手册**：[`docs/backend.md`](https://github.com/Losse-Leaf/docs/blob/main/backend.md)  
  了解单二进制启动、端口设置、SQLite 数据文件路径、Cloudflare R2 对象存储配置、本地落盘、RESTful 接口规格与数据脱敏机制。
- **Web 官方展厅设计规范**：[`docs/web.md`](https://github.com/Losse-Leaf/docs/blob/main/web.md)  
  了解棉纸与暗房双主题色盘、微噪点滤镜原理、时间流编年排版、打印排版（Print CSS）与 Web Audio 拟物音效。
- **macOS 桌面端工程规范**：[`docs/macos.md`](https://github.com/Losse-Leaf/docs/blob/main/macos.md)  
  了解状态栏常驻、全局快捷键配置、朋友圈式紧凑时间戳、受保护凭据档案（0600）与本地缓存策略。
- **移动端随行捕捉规范**：[`docs/mobile.md`](https://github.com/Losse-Leaf/docs/blob/main/mobile.md)  
  了解触觉记账小键盘输入、端侧 EXIF 智能压制、离线发件箱同步队列与生物识别解锁。
- **项目整改总台账**：[`docs/backlog.md`](https://github.com/Losse-Leaf/docs/blob/main/backlog.md)  
  查阅项目长期规则、历史已知问题整改记录与备忘索引。

---

## 二、高频排障场景与自查方案

### 1. 首次启动未能及时输入认领码
- **表现**：启动后端服务后，控制台打印的一次性认领码已超过 15 分钟时限，在浏览器输入提示已失效。
- **解决**：停止后端进程，直接重新运行二进制程序。在未认领状态下，每次重新冷启动都会重新在标准输出打印一枚全新的 15 分钟有效认领码。

### 2. 客户端扫码配对提示无法连接
- **排查步骤**：
  1. 确认手机 / 电脑与部署中枢的服务器网络互通（若为局域网部署，请确认处于同一 Wi-Fi 或已打通 Tailscale 虚拟局域网；若为公网部署，请确认域名解析与防火墙端口已放行）。
  2. 确认在 Web 端点击「添加设备」生成的配对二维码未超过 5 分钟有效窗口。
  3. 确认配对链接中包含有效的中枢地址与工单凭据。

### 3. 移动端离线记录未自动同步至中枢
- **排查步骤**：
  1. 检查移动端界面顶部是否展示离线横幅或未同步事件计数。
  2. 进入「展台 / 账户」，确认设备令牌状态有效且未在中枢被手动吊销。
  3. 下拉时间流列表手动触发增量对齐；检查系统后台是否限制了后台电量或网络活动。

---

## 三、社区支持渠道

- **功能提议与设计探讨**：请前往 [**GitHub Discussions**](https://github.com/orgs/Losse-Leaf/discussions) 发起公开探讨。
- **缺陷排查与漏洞反馈**：
  - 软件缺陷请使用 [**Bug Report 模版**](https://github.com/Losse-Leaf/.github/issues/new?template=bug_report.yml) 提交详细上下文。
  - 安全隐患请参照 [**安全政策**](https://github.com/Losse-Leaf/.github/blob/main/SECURITY.md) 提交私密报告。
