<div align="center">

# 《散页》 · Loose Leaf

**Living Archive & Personal Darkroom · 拾起散落的时光，装订成册**

*一座反功利、重真实、高质感的个人生活数字档案馆与全平台数据中枢*

[![Backend Release](https://img.shields.io/github/v/release/Losse-Leaf/backend?style=flat-square&label=Backend&color=2c2a29)](https://github.com/Losse-Leaf/backend/releases)
[![Web Release](https://img.shields.io/github/v/release/Losse-Leaf/web?style=flat-square&label=Web&color=426a51)](https://github.com/Losse-Leaf/web/releases)
[![macOS Release](https://img.shields.io/github/v/release/Losse-Leaf/MacOS?style=flat-square&label=macOS&color=3f5a4a)](https://github.com/Losse-Leaf/MacOS/releases)
[![Android Release](https://img.shields.io/github/v/release/Losse-Leaf/Android?style=flat-square&label=Android&color=8c5a3c)](https://github.com/Losse-Leaf/Android/releases)
[![License](https://img.shields.io/badge/License-MIT%20%2F%20Proprietary-181716?style=flat-square)](https://github.com/Losse-Leaf)

</div>

---

> *「不想再把自己的网络主页做成一份展示给招聘者或甲方的技术简历了。*  
> *这里是一方安静的生活自留地——将散落的日常随笔、35mm 胶卷底片、山川行迹、心愿清单与柴米油盐，一页页装订成册。」*

---

## 一、设计初衷与架构哲学

在算法信息流与模板化个人主页泛滥的今天，《散页》（Loose Leaf）试图回归**实体出版物与银盐暗房**的克制质感。它既是一个可以向访客静心展示的生活画廊，也是主理人私密掌控的个人全平台数据中枢：

- **纸墨与暗房双生美学 (Paper & Darkroom)**  
  摒弃刺眼的毛玻璃与浮夸特效，采用原生 SVG 温润棉纸微噪点、35mm 胶片装裱框（`.film-frame`）、复古裁切线与大地色系光谱；「暖调棉纸」与「暗房安全灯」双模式随系统或手动切换。声学引擎已在四端整体下线，质感交由**视觉与触觉**承担——原生端保留细腻触觉反馈，不再申请音频焦点。
- **单二进制极简分发 (Single Binary, Zero Docker)**  
  基于 `CGO_ENABLED=0` 纯 Go 架构与纯 Go 版 SQLite（WAL 并发模式），通过 `//go:embed` 将完整 Web 前端展厅熔铸进**单个可执行文件**。无需配置 Docker、Node.js 或 Nginx，无论是海外 VPS、家用 NAS 还是闲置安卓设备（Termux + Tailscale 异地组网），下载单文件赋权即跑。
- **统一认证与免密通行证 (Vesper Auth OIDC)**  
  全生态接入自建的 **Vesper Auth** 统一认证中心（OAuth 2.0 + OIDC Discovery + `S256` PKCE + Passkey），主理人凭通行证即可创刊登录，跨端单点免密；纯局域网离线部署时降级为启动时打印的 8 位一次性认领码（`XXXX-XXXX`，15 分钟有效）兜底。全程不设传统静态密码，不依赖易泄露的 `.env` 密钥文件。
- **默认私有与分层可见性 (Privacy by Design)**  
  未登录访客默认**看不到任何业务数据**。主理人仅在 Web 后台按模块开启对外只读展厅（时间流、造物与项目、山川足迹、心愿单、主理人档案、年度年鉴），即便模块已公开，单条记录仍可标记「仅自己可见」；记账流水、资产大盘、信贷分期、设备管理与存储灾备等模块**永不开放**。
- **本地主事实源与灾备镜像 (Local First, Backup Ready)**  
  中枢以 VPS 本地磁盘（`data/uploads`）为媒体的**主事实源**，提供零跨网延迟的本机直读；Cloudflare R2 与 AList 镜像作为**灾备副本**尽力而为同步。数据库仅持久化纯净相对路径（Object Key），读取时由后端下发动态签名 URL，备份与灾备恢复始终保留本地副本。
- **离线优先发件箱机制 (Offline-First Outbox Pattern)**  
  移动端与桌面伴随端内置离线优先发件箱引擎。断网或弱网环境下记录闪念、现场拍照或录入账目，数据先安全保存在本地轻量数据库中，网络就绪后由后台调度器静默续传，确保任何灵感都不因网络抖动而中断。
- **记录为一切的母体 (Record-First Architecture)**  
  生命没有孤立的足迹库或造物库。所有足迹、造物、心愿与账目均溯源于时间轴上一级发生的真实生活记录（`LifeEntry`）。二级视界联动自动生成主时间流条目，拒绝数据孤岛，杜绝极客虚假黑话与空洞装饰。

---

## 二、六大典藏卷宗

| 卷宗模块 | 核心体验与特性 |
| :--- | :--- |
| **时间流与编年归档**<br/>*Life Stream & Archive* | 支持日常随笔、胶卷相片、手艺造物与好物收藏的多态刊物排版；内置 365 天生活刻度热力图，相邻记录跨度 $\ge 14$ 天自动生成「岁月留白」呼吸切线。 |
| **山川行迹与两级抽屉**<br/>*Travel Atlas & Drawers* | 采用中国国家标准 Albers 等面积圆锥投影，绘制**省＋市两级墨色阶点亮地图**；点击任意已点亮省市，平滑滑出聚合「履迹简志、菲林画廊、散页随笔、属地账单光谱」的四重回忆抽屉。 |
| **三维心愿单与归册仪式**<br/>*Three-State Wishlist* | 涵盖「心仪好物 / 山川旅程 / 人生里程碑」；支持**在愿蓄水池**、**理性拔草**（正向统计因克制欲望而省下的财富）与**圆满归册**（一键事务联动生成支出账单、时间流随笔并点亮城市足迹）。 |
| **年度生活年鉴五幕画卷**<br/>*Annual Almanac* | 自动提炼「岁月卷首、山川行迹、向往风物、人间烟火、高光画廊」五幕岁末长卷；深度定制 `@media print` 打印样式，一键隐去交互控件、铺展为标准 A4 纸张，随时导出高清 PDF 或装订成实体书。 |
| **柴米油盐与资产中枢**<br/>*Ledger & Assets Hub* | 全链路 `cents`（整型分）无损记账；构建「在用固定资产 + 流动资金池 - 待还分期负债」三层净资产模型；支持设备二手回血核销与多信贷渠道独立还款日追踪。 |
| **暗房媒体与双模存储**<br/>*Local Media & R2 Backup* | 本地磁盘为主事实源、Cloudflare R2 与 AList 镜像为灾备副本；未配置云存储时开箱直存本地磁盘（`data/uploads`），配置后无缝切换为端侧动态预签名临时 URL与服务端缩略图服务。 |

---

## 三、生态仓库矩阵 (Repositories)

```mermaid
graph TD
    subgraph CoreHub["单一事实来源 · 数据中枢 (Core SSOT Hub)"]
        Backend["<b>Losse-Leaf/backend</b><br/>Go + SQLite (WAL) + 本地/R2/AList 存储<br/>单二进制内嵌分发 · ETag 缓存协商"]
    end

    subgraph Identity["统一认证中心 (Identity)"]
        Auth["<b>Vesper Auth</b><br/>OAuth 2.0 + OIDC Discovery + S256 PKCE<br/>Passkey 通行证 · 白名单准入"]
    end

    subgraph Clients["多端交互矩阵 (Multi-Platform Clients)"]
        Web["<b>Losse-Leaf/web</b><br/>Vue 3 + Vite + Tailwind CSS 4<br/>公开画廊 · 实体书排版 · 综合管理"]
        Mac["<b>Losse-Leaf/MacOS</b><br/>Swift 6 / SwiftUI + AppKit<br/>菜单栏常驻 Popover · 全局快捷捕捉"]
        Android["<b>Losse-Leaf/Android</b><br/>Kotlin / Jetpack Compose / Room<br/>口袋触觉记账 · 现场暗房 · 离线发件箱"]
    end

    subgraph Specs["全平台规范与知识库 (Standards & Specs)"]
        Docs["<b>Losse-Leaf/docs</b><br/>架构蓝图 · 跨端设计系统 · API 契约"]
        Github["<b>Losse-Leaf/.github</b><br/>组织主页 · 社区健康公约 · 规范模版"]
    end

    Auth -->|签发会话与设备凭证| Backend
    Backend <-->|RESTful API v1 / 离线同步| Web
    Backend <-->|RESTful API v1 / 增量同步| Mac
    Backend <-->|RESTful API v1 / 离线优先发件箱| Android

    Docs -.->|设计规范与接口契约| Clients
    Docs -.->|架构规范与数据精度| Backend
```

| 仓库 | 定位与职责 | 技术栈 | 最新版本 |
| :--- | :--- | :--- | :---: |
| **[`Losse-Leaf/backend`](https://github.com/Losse-Leaf/backend)** | **后端数据中枢与单二进制分发引擎**<br/>提供 RESTful API v1、设备令牌与统一认证接入、SQLite WAL 持久化、本地主存储与 R2 / AList 灾备、缩略图服务及内嵌 Web 静态服务 | `Go` · `Gin` · `GORM` · `SQLite` · `Cloudflare R2` | [![Backend Release](https://img.shields.io/github/v/release/Losse-Leaf/backend?style=flat-square&label=&color=2c2a29)](https://github.com/Losse-Leaf/backend/releases) |
| **[`Losse-Leaf/web`](https://github.com/Losse-Leaf/web)** | **Web 官方展厅与后台管理终端**<br/>纸墨与暗房双主题、全自研纸本表单控件、六大业务视图与全站唯一全量管理中枢 | `Vue 3` · `TypeScript` · `Vite` · `Tailwind CSS 4` | [![Web Release](https://img.shields.io/github/v/release/Losse-Leaf/web?style=flat-square&label=&color=426a51)](https://github.com/Losse-Leaf/web/releases) |
| **[`Losse-Leaf/MacOS`](https://github.com/Losse-Leaf/MacOS)** | **macOS 桌面伴随工作台**<br/>Menubar 常驻快速捕捉、全局快捷键呼出 (`Cmd+Shift+L`)、紧凑朋友圈式时间戳、受保护凭据档案 (`0600`) | `Swift 6` · `SwiftUI` · `AppKit` | [![macOS Release](https://img.shields.io/github/v/release/Losse-Leaf/MacOS?style=flat-square&label=&color=3f5a4a)](https://github.com/Losse-Leaf/MacOS/releases) |
| **[`Losse-Leaf/Android`](https://github.com/Losse-Leaf/Android)** | **Android 随行口袋暗房与记账本**<br/>触觉大键位记账键盘、自然语义快记、通知监听自动记账、端侧 EXIF 智能压制、离线优先发件箱 (Outbox Engine)、生物识别安全锁 | `Kotlin` · `Jetpack Compose` · `Room` · `WorkManager` | [![Android Release](https://img.shields.io/github/v/release/Losse-Leaf/Android?style=flat-square&label=&color=8c5a3c)](https://github.com/Losse-Leaf/Android/releases) |
| **[`Losse-Leaf/docs`](https://github.com/Losse-Leaf/docs)** | **全平台架构设计与工程规范专著**<br/>生态演进蓝图、后端与多端协同规范、Web 展厅设计系统、桌面与移动端开发指南、整改总台账 | `Markdown` · `Mermaid` · `Architecture Specs` | 主干基准 |
| **[`Losse-Leaf/.github`](https://github.com/Losse-Leaf/.github)** | **组织级配置与社区健康中心**<br/>全组织默认社区公约、贡献指南、安全政策、PR 与 Issue 模版 | `Community Health` · `Issue Forms` | 主干基准 |

---

## 四、极速启动 (Quick Start)

无需安装 Go、Node.js、Docker 或配置任何复杂的数据库环境，直接从 [**Backend Releases**](https://github.com/Losse-Leaf/backend/releases) 下载对应系统的单二进制文件即可运行：

### 1. 运行中枢服务

```bash
# 以 Linux x86_64 为例（macOS Apple Silicon 请下载 looseleaf-darwin-arm64）
curl -fLO https://github.com/Losse-Leaf/backend/releases/latest/download/looseleaf-linux-amd64
chmod +x looseleaf-linux-amd64

# 直接启动（默认监听 :8088，自动在 ./data 下生成 SQLite 库与本地媒体目录）
./looseleaf-linux-amd64
```

### 2. 两条入场通道

《散页》的上层接入支持「统一认证主通道 ＋ 局域网一次性认领码兜底」双形态：

- **统一认证主通道（生产默认，`OIDC_ENABLED=true`）**  
  接入自建 **Vesper Auth**（`https://auth.starryheavens.uk`）。主理人在浏览器完成通行证验证（OAuth 2.0 + OIDC Discovery + `S256` PKCE + Passkey）并命中 `OIDC_ALLOWED_SUB` 白名单后，后端在同一事务内自动完成创刊激活并下发 30 天 `HttpOnly` 会话 Cookie，全程无需翻查认领码。若同浏览器已在其他 `*.starryheavens.uk` 子域登录过 Vesper Auth，可无感进入主理人模式。

- **局域网离线兜底（`OIDC_ENABLED=false`）**  
  纯离线部署时后端在标准输出打印 8 位一次性认领码：

  ```text
  ======================================================
    《散页》首次运行就绪！请在浏览器打开中枢完成初始配对：
    http://localhost:8088
    一次性入网认领码: 8A2F-9C4D (15 分钟内有效)
  ======================================================
  ```

  在浏览器输入认领码即认领首台设备；其余设备沿用配对工单握手接入。

### 3. 多端接入

打开 [**macOS 客户端**](https://github.com/Losse-Leaf/MacOS/releases) 或 [**Android 随行端**](https://github.com/Losse-Leaf/Android/releases)，在门禁页点击「通过 Vesper Auth 通行证一键接入」：客户端拉起系统浏览器完成通行证验证，中枢签发一次性配对工单（90 秒有效）并经 `looseleaf://` 深链接交回客户端核销落盘，全程无需手工输入任何码。纯局域网兜底模式下，首台设备由 Web 浏览器输入启动时打印的认领码认领，其余设备沿用配对工单握手接入。

---

## 五、生产部署形态

- **海外 VPS + 单二进制**：线上监听 `127.0.0.1` 配合本机 Nginx 反向代理处理 TLS 与端口转发，无需 Docker / Node.js 运行时。
- **免备案**：海外部署不需要 ICP 与公安备案，站点任何位置（含页脚）均不展示备案号。
- **标准主域**：生产主域统一为 `https://leaf.starryheavens.uk`，统一认证服务为 `https://auth.starryheavens.uk`。

---

## 六、跨端工程规范核心准则

无论面向哪个平台开发，参与者均严格遵守以下核心法则（权威定义见 [`docs/README.md`](https://github.com/Losse-Leaf/docs) §四）：

1. **单一事实来源 (SSOT)**：后端 SQLite 数据库是所有状态的唯一权威；各客户端本地数据库仅作为只读缓存与待同步发件箱。
2. **金额严格以整数分流转 (Cents Precision)**：全链路严禁浮点数，金额单位统一为分（`int64`）。
3. **弹性时间与北京时间基准 (FlexTime UTC+8)**：时间格式弹性解析，显示基准统一锁定为中国北京时间（UTC+8），消除跨时区漂移。
4. **媒体上传双通道**：Web 只走统一上传接口，原生端走预签名直传，业务表只落相对 `object_key`。
5. **实体书与暗房相纸质感**：严格遵循自然大地色盘（棉纸底色、深暖墨黑、暖赭石、苔藓绿等），杜绝塑料渐变与刺眼特效；原生端不得硬编码色值。
6. **离线优先发件箱**：弱网与断网环境下即时记录，数据先落本地发件箱，恢复后按时序静默补传。
7. **代码质量准则**：低耦合高内聚、拒绝重复实现、字段级单一数据源、不留兼容层、零冗余字段、禁止假数据兜底。
8. **记录为一切的母体 (Record-First)**：所有足迹、造物、心愿、记账行为均溯源并伴生于一级生活档案（`LifeEntry`）。
9. **隐私与可见性分层**：全站默认私有，模块级公开开关与单条私密兜底叠加生效。
10. **统一契约与减法边界**：实体与枚举语义以统一契约为准，低频重管理统一收归 Web，原生端聚焦高频捕捉与轻量回看。

更多详尽规范请查阅 [**全平台架构设计与工程规范专著 (docs)**](https://github.com/Losse-Leaf/docs)。

---

## 七、参与装帧 (Contributing)

《散页》欢迎认同其设计理念的创作者与工程师共同雕琢：

- 查阅 [**全组织贡献指南 (CONTRIBUTING.md)**](https://github.com/Losse-Leaf/.github/blob/main/CONTRIBUTING.md) 了解开发流程与提交要求。
- 查阅 [**社区公约 (CODE_OF_CONDUCT.md)**](https://github.com/Losse-Leaf/.github/blob/main/CODE_OF_CONDUCT.md) 维护宁静、专注、真诚的交流氛围。
- 发现漏洞或安全隐患请参照 [**安全政策 (SECURITY.md)**](https://github.com/Losse-Leaf/.github/blob/main/SECURITY.md) 执行负责任披露。

---

<div align="center">

*Paper & Film · Living Archive · Built with quiet craftsmanship.*

</div>
