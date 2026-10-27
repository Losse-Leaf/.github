# 《散页》（Loose Leaf）全平台贡献指南

> **Living Archive · 拾起散落的时光，装订成册**  
> 本指南适用于《散页》组织旗下所有代码仓库（包括后端中枢、Web 展厅端、macOS 桌面伴随端、Android 随行端及文档专著库）。

---

## 一、欢迎与创作哲学

感谢你关注《散页》（Loose Leaf）项目。

在算法推荐、信息洪流与快餐式软件盛行的当下，《散页》试图打造一方反功利、重真实、高质感的个人生活数字档案馆。主理人在此沉淀日常随笔、35mm 胶卷底片、山川行迹、心愿清单与真实的柴米油盐收支。

我们对待每一行代码，如同手工装订实体刊物般克制与严谨。我们欢迎所有认同这一愿景的工程师、设计师与文字创作者参与雕琢。在着手编写代码或发起 PR 之前，请务必阅读本指南，理解并践行我们的核心工程约定。

---

## 二、生态仓库与职责矩阵

《散页》由一个统一的数据中枢与三大核心终端构成，各仓库边界清晰、权责明确：

| 仓库名称 | 技术栈 | 职责定位与核心特性 |
| :--- | :--- | :--- |
| **[`Losse-Leaf/backend`](https://github.com/Losse-Leaf/backend)** | Go / Gin / SQLite / R2 | **单一事实来源 (SSOT) & 单二进制分发引擎**<br/>RESTful API v1、母子设备令牌鉴权体系、内嵌 Web 前端、CatmullRom 缩略图服务、纯 Go 无 CGO 依赖。 |
| **[`Losse-Leaf/web`](https://github.com/Losse-Leaf/web)** | Vue 3 / TS / Tailwind CSS 4 | **Web 官方展厅与后台管理端**<br/>纸墨与暗房双主题、微噪点滤镜、六大业务卷宗、Web Audio 拟物声学引擎、Composable 单例状态驱动。 |
| **[`Losse-Leaf/MacOS`](https://github.com/Losse-Leaf/MacOS)** | Swift 6 / SwiftUI / AppKit | **桌面无感伴随工作台**<br/>Menubar 常驻快速捕捉 Popover、全局快捷键 (`Cmd+Shift+L`)、朋友圈式紧凑时间戳、受保护本地凭据档案 (`0600`)。 |
| **[`Losse-Leaf/Android`](https://github.com/Losse-Leaf/Android)** | Kotlin / Compose / Room | **随行第一现场口袋暗房与记账本**<br/>触觉大键位记账键盘、端侧 EXIF 智能压制、离线优先发件箱 (Outbox Engine)、生物识别安全门禁。 |
| **[`Losse-Leaf/docs`](https://github.com/Losse-Leaf/docs)** | Markdown / Mermaid | **全平台架构规范与工程专著**<br/>生态演进蓝图、跨端设计系统映射、接口详细契约、整改总台账。 |
| **[`Losse-Leaf/.github`](https://github.com/Losse-Leaf/.github)** | Community Health | **组织级配置与社区健康中心**<br/>全组织默认社区规范、贡献指南、安全政策、Issue / PR 模版。 |

---

## 三、跨端核心工程约定 (Core Tenets)

无论面向哪一个平台实现，所有贡献者**必须严格遵守**以下七大黄金法则：

### 1. 单一事实来源 (Single Source of Truth, SSOT)
- 后端 SQLite 数据库是全局数据的唯一权威。
- 客户端的本地数据库（如 Android 的 Room、macOS 的本地存储）仅作为**高性能只读缓存**与**离线待同步发件箱**，不可在本地擅自篡改服务端的权威状态。

### 2. 金额严格以整数分流转与计算 (Cents Precision)
- 所有涉及货币金额（收入、支出、净资产、预算等）的字段，**全链路严禁使用浮点数 (float/double)** 存储与传输。
- 统一采用 64 位整型（`int64`），单位为**分**（Cents）。例如：`¥18.50` 传输与存储均为 `1850`。
- 客户端仅在用户输入界面负责倍乘转换，在渲染呈现时进行两阶小数格式化。

### 3. 弹性时间解析与中国北京时间基准 (FlexTime UTC+8)
- 服务端支持弹性解析多种时间输入格式（ISO8601、RFC3339、纸本点号格式 `YYYY.MM.DD HH:mm`）。
- **时区权威基准统一为中国北京时间（UTC+8）**。凡不带时区后缀的时间字符串一律按北京时间解释。客户端展示端无论用户设备处于何种本地时区，均还原为北京时间对齐呈现，确保跨时区与海外部署零漂移。

### 4. 实体书与银盐暗房质感 (Paper & Film Aesthetic)
- 界面视觉严格遵从自然大地色盘（棉纸底色、深暖墨黑、暖赭石、苔藓绿等），严禁出现冰冷的高反差、塑料渐变或荧光霓虹特效。
- 各客户端 UI 代码中**严禁硬编码十六进制颜色字面量**，所有颜色必须引用各平台设计令牌（Semantic Tokens）。

### 5. 离线优先发件箱模式 (Offline-First Outbox Pattern)
- 原生端（macOS 与 Android）必须具备断网环境下无阻碍记录闪念与记账的能力。
- 本地变动先以事件形式进入本地 Outbox 队列，网络连通后按严格时序后台静默同步至服务端。

### 6. 记录为一切的母体 (Record-First Architecture)
- 生命没有孤立的足迹库或造物库。所有足迹、造物、心愿、记账行为均溯源于一级发生的真实生活记录（`LifeEntry`）。
- 从二级视界（如足迹打卡、开启造物）录入时，必须自动伴生创建对应的一级条目并写入主时间流；时间流记录带有地理或造物标签时，下游视图自动收录，拒绝数据孤岛。

### 7. 工程质量与零债务准则 (Engineering Quality)
- **不留过渡兼容层**：项目处于快速演进期，严禁为历史临时格式或废弃接口保留冗余分支。
- **零冗余死字段**：模型中的字段必须有明确的写入方与读取方，禁止仅用于伪造示例的冗余定义。
- **严格零 Emoji 规范**：为了保持《散页》典雅、克制、书卷气的整体风格，无论是代码注释、Git 提交信息、UI 文案还是系统提示，**一律严禁出现 Emoji 表情符号**。

---

## 四、本地开发环境就绪

### 1. 后端中枢 (Backend)
- **环境依赖**：Go 1.22 及以上版本。
- **本地启动**：
  ```bash
  cd backend
  cp .env.example .env
  go run main.go
  ```
- **质量验证**：
  ```bash
  go vet ./...
  go test -v ./...
  CGO_ENABLED=0 go build -v -o /dev/null .
  ```

### 2. Web 展厅端 (Web)
- **环境依赖**：Node.js 20+ 及 npm。
- **本地启动**：
  ```bash
  cd web
  npm install
  npm run dev
  ```
- **质量验证**：
  ```bash
  npm run build
  ```

### 3. macOS 桌面端 (macOS)
- **环境依赖**：macOS 14+，Xcode 15+，Swift 6 兼容环境。
- **编译与验证**：
  ```bash
  cd mac
  swift build -Xswiftc -warnings-as-errors
  swift test
  ```

### 4. Android 随行端 (Android)
- **环境依赖**：JDK 17，Android SDK 35。
- **编译与验证**：
  ```bash
  cd android
  ./gradlew testPublicDebugUnitTest testLanDebugUnitTest
  ./gradlew assembleLanDebug
  ```

---

## 五、Git 分支与提交规范

### 1. 分支策略
- `main` 为主分支，随时处于可发布状态。
- 新特性开发与缺陷修复请从 `main` 切出新分支，命名格式推荐：
  - `feat/<feature-name>`
  - `fix/<issue-name>`
  - `refactor/<module-name>`
  - `docs/<doc-name>`

### 2. 提交信息规范 (Conventional Commits)
提交信息遵循约定式提交规范，格式如下：

```
<type>(<scope>): <subject>

[optional body]

[optional footer]
```

- **Type（类型）**：
  - `feat`: 新增功能特性
  - `fix`: 修复缺陷或异常
  - `refactor`: 重构优化（既不新增功能也不修复缺陷）
  - `perf`: 性能调优
  - `docs`: 仅限文档变更
  - `test`: 增加或修正单元测试
  - `chore`: 构建配置、依赖或工具链调整
- **Scope（作用域）**：明确受影响的子系统（如 `backend`, `web`, `mac`, `android`, `stream`, `ledger` 等）。
- **Subject（简述）**：用克制、精准的中文简述修改，末尾不加句号，**严禁添加任何 Emoji**。
- **示例**：
  - `feat(ledger): 支持信贷渠道独立还款日追踪`
  - `fix(stream): 修复离开组合树时协程取消被误报为拉取失败的问题`
  - `docs(api): 更新离线发件箱增量拉取游标协议说明`

---

## 六、Pull Request 规范与自查清单

在提交 Pull Request 前，请确保完成以下自查：

1. **已关联 Issue**：说明本次变更解决的具体问题或关联的议题编号。
2. **本地测试与门禁全绿**：针对目标模块运行完整的单元测试和构建命令，确保 CI 零失败。
3. **无硬编码与无浮点金额**：检查涉及金额计算处是否全链路采用 `cents`（分）；检查 UI 是否使用了语义设计令牌。
4. **无未清理的代码遗留**：无注掉的大段死代码、无调试用的 `console.log` / `println`、无未清理的临时兼容分支。
5. **符合零 Emoji 规范**：检查 PR 标题、描述正文与所有修改代码中均无 Emoji。

---

## 七、交流与支持

- 若发现软件缺陷，请使用 [**Bug Report 模版**](https://github.com/Losse-Leaf/.github/issues/new?template=bug_report.yml) 提交议题。
- 若有新的设计思考或功能提议，请先在 [**GitHub Discussions**](https://github.com/orgs/Losse-Leaf/discussions) 发起探讨，以便充分评估其与《散页》核心美学的契合度。
