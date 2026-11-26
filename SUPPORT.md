# 《散页》（Loose Leaf）支持与帮助指南

> **Support & Help Guidelines · 宁静翻阅，答疑解惑**

欢迎查阅《散页》（Loose Leaf）支持中心。在使用本项目的单二进制服务端、Web 展厅、macOS 桌面工作台或 Android 随行端时，若遇到任何配置、登录或使用疑问，可按照以下索引寻求帮助。

---

## 一、权威文档专著地图

在提交咨询或报告问题前，请优先阅读对应专著文档，大多数常见疑问均在其中详细解答：

- **全平台生态架构与工程总纲**：[`docs/README.md`](https://github.com/Losse-Leaf/docs/blob/main/README.md)  
  了解四端协同边界、十大核心约定、跨端设计语言映射、离线优先发件箱机制与部署形态。
- **后端中枢开发与部署手册**：[`docs/backend.md`](https://github.com/Losse-Leaf/docs/blob/main/backend.md)  
  了解单二进制启动、端口设置、SQLite 数据文件路径、本地主存储与 Cloudflare R2 灾备配置、RESTful 接口规格与数据脱敏机制。
- **Web 官方展厅设计规范**：[`docs/web.md`](https://github.com/Losse-Leaf/docs/blob/main/web.md)  
  了解棉纸与暗房双主题色盘、微噪点滤镜原理、时间流编年排版与打印排版（Print CSS）。
- **macOS 桌面端工程规范**：[`docs/macos.md`](https://github.com/Losse-Leaf/docs/blob/main/macos.md)  
  了解状态栏常驻、全局快捷键配置、朋友圈式紧凑时间戳、受保护凭据档案（0600）与本地缓存策略。
- **移动端随行捕捉规范**：[`docs/mobile.md`](https://github.com/Losse-Leaf/docs/blob/main/mobile.md)  
  了解触觉记账小键盘输入、自然语义快记与通知监听自动记账、端侧 EXIF 智能压制、离线发件箱同步队列与生物识别解锁。
- **项目整改总台账**：[`docs/backlog.md`](https://github.com/Losse-Leaf/docs/blob/main/backlog.md)  
  查阅项目长期规则、历史已知问题整改记录与备忘索引。

> 各端的当前版本号一律以各自仓库的 Release tag 为准（`backend`、`web`、`MacOS`、`Android`），文档正文不罗列版本号以免过时。

---

## 二、高频排障场景与自查方案

### 1. 统一认证通行证校验不通过
- **表现**：点击「通过 Vesper Auth 通行证」后停在验证页，或提示账号不在准入名单内。
- **自查步骤**：
  1. 确认当前中枢已接入自建 Vesper Auth（`OIDC_ENABLED=true`），且认证服务地址与生产主域 `auth.starryheavens.uk` 配置一致。
  2. 确认当前账号的 `sub` 已写入后端的 `OIDC_ALLOWED_SUB` 白名单；白名单外的账号即使通过 Passkey 验证也会被拒绝。
  3. 确认浏览器与系统时间准确，时间漂移会导致令牌校验失败。
  4. 若属纯局域网离线部署（`OIDC_ENABLED=false`），请改走第 2 条兜底通道。

### 2. 一次性认领码提示已失效
- **表现**：在纯局域网离线部署中，启动时打印的 8 位认领码（`XXXX-XXXX`）已超过 15 分钟时限，或连续输错 5 次后被作废。
- **解决**：停止后端进程并重新运行二进制程序。在未认领状态下，每次重新冷启动都会重新在标准输出打印一枚全新的认领码；若用 systemd 部署，用 `journalctl -u loose-leaf` 查看。

### 3. 客户端接入或登录失败
- **排查步骤**：
  1. 确认手机 / 电脑与部署中枢的网络互通（局域网部署需处于同一 Wi-Fi 或已打通 Tailscale 虚拟局域网；公网部署需确认域名解析与防火墙端口已放行）。
  2. 确认走的是**统一认证通道**：客户端在门禁页拉起系统浏览器完成 Vesper Auth 通行证验证后，中枢签发一次性配对工单（90 秒有效）并经 `looseleaf://` 深链接交回客户端核销；工单过期或跨端接力失败时重新点击一次即可。
  3. 确认客户端填写的**中枢地址**正确且协议合法（公网中枢必须为 `https`）；macOS 与 Android 都会对回跳链接做二次校验，非预期服务器会要求用户手动确认。
  4. 若客户端在中枢侧已被吊销，登录会直接失败并阻断本地离线队列，需由主理人重新放行后再接入。

### 4. 移动端离线记录未自动同步至中枢
- **排查步骤**：
  1. 检查移动端界面顶部是否展示离线横幅或未同步事件计数。
  2. 确认本机设备状态有效且未在中枢被手动吊销（可由主理人通过中枢设备管理接口核对）。
  3. 下拉时间流列表手动触发增量对齐；检查系统后台是否限制了后台电量或网络活动。
  4. 确认中枢侧未处于存储灾备恢复期门禁（恢复期间写入会被暂时拒绝）。

### 5. 访客打开站点后看不到任何内容
- **说明**：这是预期行为，不是故障。《散页》**默认全站私有**，访客仅在主理人于 Web 后台开启对应模块的对外只读展厅后，才能看到该模块内容；记账、资产、信贷与设备管理等模块永不开放。

---

## 三、社区支持渠道

- **功能提议与设计探讨**：请使用 [**特性提议模版**](https://github.com/Losse-Leaf/.github/issues/new?template=feature_request.yml) 提交公开探讨，描述现有痛点、提议方案与美学契合度考量。
- **缺陷排查与漏洞反馈**：
  - 软件缺陷请使用 [**Bug Report 模版**](https://github.com/Losse-Leaf/.github/issues/new?template=bug_report.yml) 提交详细上下文。
  - 数据同步与设备接入异常请使用 [**Sync Issue 模版**](https://github.com/Losse-Leaf/.github/issues/new?template=sync_issue.yml)。
  - 安全隐患请参照 [**安全政策**](https://github.com/Losse-Leaf/.github/blob/main/SECURITY.md) 提交私密报告。
