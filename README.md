# 《散页》（Loose Leaf）· 组织配置与社区健康中心

> **Organization Defaults & Community Health Hub**  
> 归属组织: [https://github.com/Losse-Leaf](https://github.com/Losse-Leaf)  
> 维护路径: [`Losse-Leaf/.github`](https://github.com/Losse-Leaf/.github)

---

## 一、仓库定位与职责

本仓库为 GitHub 组织 `Losse-Leaf` 的专属全局配置仓库（Special `.github` Repository），承担全组织的公共基准设定：

1. **组织官方主页展板**：维护位于 [`profile/README.md`](profile/README.md) 的全景画卷，向全球访客宁静呈现《散页》的设计初衷、生态全景矩阵、六大典藏卷宗与极速启动指南。
2. **组织级社区健康默认文件**：为组织内所有下游代码仓库（[`backend`](https://github.com/Losse-Leaf/backend)、[`web`](https://github.com/Losse-Leaf/web)、[`MacOS`](https://github.com/Losse-Leaf/MacOS)、[`Android`](https://github.com/Losse-Leaf/Android)、[`docs`](https://github.com/Losse-Leaf/docs)）提供统一生效的贡献公约、安全政策、支持指南以及 Issue / PR 规范模版。

---

## 二、目录结构全景

```text
.github/
├── profile/
│   └── README.md                # 组织主页全景展示画卷 (Organization Profile)
├── ISSUE_TEMPLATE/
│   ├── bug_report.yml           # 结构化缺陷报告模版 (Issue Form)
│   ├── feature_request.yml      # 特性与设计提议模版 (Issue Form)
│   ├── sync_issue.yml           # 数据同步与设备配对故障专用模版
│   └── config.yml               # 议题分类导航与外部支持重定向配置
├── CONTRIBUTING.md               # 全平台开发与贡献指南 (含七大核心黄金法则)
├── CODE_OF_CONDUCT.md           # 社区守则与创作公约 (宁静、克制、相互尊重)
├── SECURITY.md                  # 全平台安全政策与多层防线架构
├── SUPPORT.md                   # 支持中心与常见疑难排查手册
├── PULL_REQUEST_TEMPLATE.md     # 跨端变更 PR 提交规范与核验清单
└── README.md                    # [本文件] 本仓库维护指引
```

---

## 三、全局健康文件继承规则

根据 GitHub 社区标准，组织级 `.github` 仓库中的健康文件将被组织内所有公开仓库自动继承：

- 当某个下游仓库（如 `Losse-Leaf/backend`）未单独定义其自身的 `CONTRIBUTING.md` 时，GitHub 将自动应用本仓库中的 [`CONTRIBUTING.md`](CONTRIBUTING.md)。
- 当用户在任一仓库点击「New Issue」时，GitHub 将自动呈现本仓库定义的统一结构化 Issue Forms。
- 当用户发起 Pull Request 时，GitHub 将自动注入本仓库的 [`PULL_REQUEST_TEMPLATE.md`](PULL_REQUEST_TEMPLATE.md) 自查清单。

---

## 四、核心工程准则提示

所有提交至本仓库或下游各端的文本与代码，均须严格遵循《散页》核心规范：

1. **严格零 Emoji 规范**：全站所有文档、模版、注释与提交信息中严禁使用任何 Emoji 表情。
2. **实体书与银盐暗房质感**：语言温润克制、排版严整优雅，秉持长期主义手工艺精神。
3. **数据主权与隐私第一**：所有安全与鉴权机制均服务于保护个人真实生活痕迹。
