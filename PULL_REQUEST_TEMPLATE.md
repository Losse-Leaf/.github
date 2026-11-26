## 变更概要 (Summary)

请在此简明扼要地概括本次 Pull Request 的核心目的与修改内容。

---

## 关联议题 (Related Issues)

- Closes #
- Relates to #

---

## 影响子系统 (Subsystems Involved)

请勾选本次变更涉及的子系统：

- [ ] 后端中枢 (Backend - Go / SQLite)
- [ ] Web 官方展厅 (Web - Vue 3 / Vite / Tailwind)
- [ ] macOS 桌面伴随端 (macOS - Swift / SwiftUI)
- [ ] Android 随行端 (Android - Kotlin / Compose)
- [ ] 统一认证接入 (Auth - Vesper Auth OIDC / 设备配对)
- [ ] 媒体存储与灾备 (Storage - 本地主存储 / R2 / AList)
- [ ] 文档专著与规范 (Docs)
- [ ] CI / 构建与发布流水线 (Workflows / Infrastructure)

---

## 变更类型 (Type of Change)

- [ ] 缺陷修复 (Bug fix)
- [ ] 新特性 (New feature)
- [ ] 重构优化 (Refactoring)
- [ ] 性能调优 (Performance optimization)
- [ ] 规范文档补充 (Documentation)
- [ ] 依赖或工具链升级 (Tooling / Dependencies)

---

## 跨端核心工程约定自查清单 (Tenets Compliance Checklist)

在请求审查前，请逐一确认并勾选符合《散页》十大核心法则（权威定义见 [`docs/README.md`](https://github.com/Losse-Leaf/docs) §四）：

- [ ] **单一事实来源 (SSOT)**：数据状态以服务端 SQLite 为权威，本地数据库未越权篡改状态。
- [ ] **货币分级精度 (Cents)**：涉及金额的流转与计算严格使用 `int64`（分），无任何浮点数隐患。
- [ ] **时间基准 (FlexTime UTC+8)**：时间解析具有弹性，渲染与边界计算统一以中国北京时间（UTC+8）为基准，未直接调用本地时区 getter。
- [ ] **媒体上传双通道**：Web 只走统一上传接口，原生端走预签名直传，业务表只落相对 `object_key`。
- [ ] **设计系统契约**：严格遵循自然大地色盘与实体书微噪点质感，界面代码无硬编码颜色字面量。
- [ ] **离线优先发件箱**：弱网与断网下的本地写入可落盘可补传，失败事件不静默丢弃。
- [ ] **记录为母体 (Record-First)**：二级视界（足迹/造物/心愿/账本）与一级生活档案（LifeEntry）联动闭环。
- [ ] **隐私与可见性分层**：默认私有、模块公开开关与单条私密兜底语义一致，访客视角字段已剥离。
- [ ] **无兼容层与无冗余字段**：无注掉的大段死代码、无废弃过渡兼容层、无无消费者的冗余字段、无假数据兜底。
- [ ] **严格零 Emoji 规范**：代码注释、提交信息、UI 文案与本 PR 内容中**完全不含任何 Emoji 表情**。
- [ ] **文档同步**：若涉及实体字段、枚举语义、接口契约或目录结构，已在同批改动中同步 `docs` 对应专著。
- [ ] **测试验证**：本地单元测试全量通过，静态分析检查通过。

---

## 验证与测试证据 (Verification Evidence)

请附上本地运行测试通过的日志输出、终端构建结果或验证截图（无 Emoji）：

```text
[在这里粘贴本地测试与构建的命令输出]
```
