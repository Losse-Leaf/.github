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

在请求审查前，请逐一确认并勾选符合《散页》核心法则：

- [ ] **货币分级精度 (Cents)**：涉及金额的流转与计算严格使用 `int64`（分），无任何浮点数隐患。
- [ ] **时间基准 (FlexTime UTC+8)**：时间解析具有弹性，渲染与边界计算统一以中国北京时间（UTC+8）为基准。
- [ ] **单一事实来源 (SSOT)**：数据状态以服务端 SQLite 为权威，本地数据库未越权篡改状态。
- [ ] **设计系统契约**：严格遵循自然大地色盘与实体书微噪点质感，无硬编码颜色字面量。
- [ ] **记录为母体 (Record-First)**：二级视界（足迹/造物/心愿/账本）与一级生活档案（LifeEntry）联动闭环。
- [ ] **代码整洁与零债务**：无注掉的大段死代码、无废弃过渡兼容层、无无消费者的冗余字段。
- [ ] **严格零 Emoji 规范**：代码注释、提交信息、UI 文案与本 PR 内容中**完全不含任何 Emoji 表情**。
- [ ] **测试验证**：本地单元测试全量通过，静态分析检查通过。

---

## 验证与测试证据 (Verification Evidence)

请附上本地运行测试通过的日志输出、终端构建结果或验证截图（无 Emoji）：

```text
[在这里粘贴本地测试与构建的命令输出]
```
