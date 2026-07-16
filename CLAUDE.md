# CLAUDE.md - 背单词网站项目指引

## 项目位置
`e:\英语单词背诵\`

## 项目简介
为大学生用户开发的英语背单词单页网站（类似"不背单词"），单个 HTML 文件，双击即用。

## 开发原则
1. **分步推进**：按 Phase 逐步开发，每完成一个 Phase 需用户确认后再进入下一阶段
2. **每日记录**：每次开发后在 `dev-logs/` 中更新当日日志
3. **文档先行**：所有需求、设计、技术变更先更新 `docs/` 中的文档
4. **稳定优先**：每个 Phase 独立可验证，不一次性大量改动

## 标准文件路径

| 文件 | 路径 | 说明 |
|------|------|------|
| 需求文档 | `docs/requirements.md` | 功能与非功能需求 |
| 技术方案 | `docs/technical.md` | 技术选型、数据结构、算法 |
| 设计规范 | `docs/design.md` | 配色、排版、组件、布局 |
| 执行步骤 | `docs/execution.md` | 分阶段任务清单 |
| 开发日志 | `dev-logs/YYYY-MM-DD.md` | 每日开发记录 |
| 最终产品 | `背单词.html` | 单文件网站 |

## 技术约束
- 纯前端：HTML + CSS + JavaScript（无框架，无 Node.js 依赖）
- 数据存储：浏览器 localStorage
- 发音：Web Speech API（浏览器内置）
- 目标浏览器：Chrome / Edge / Firefox
- 操作系统：Windows 10/11

## 工作流程
1. 阅读 `docs/execution.md` 了解当前进度
2. 阅读 `docs/requirements.md` 和 `docs/design.md` 确认需求
3. 开发当前 Phase 的任务
4. 完成后更新 `docs/execution.md` 勾选完成项
5. 更新 `dev-logs/` 当日日志
6. 请用户验证后进入下一 Phase

## Phase 开发顺序
1. ✅ 项目基础设施（已完成）
2. ⏳ 词库数据准备（下一步）
3. 基础 UI 框架
4. 核心答题功能
5. 发音功能
6. 错题本功能
7. 搜索功能
8. 收尾与优化

## 注意事项
- 用户非技术背景，代码注释尽量清晰
- 所有文字使用中文
- 词库为四级核心词汇
- 不要在未经用户确认的情况下跨 Phase 开发
