# Job Tool

Job Tool 是一个本地优先的简历与求职工具。桌面端基于 Tauri 2、React、Vite 和 Rust 构建；移动端基于 React Native + Expo，并通过共享数据层与桌面端保持一致。应用不需要登录，也不依赖服务端账号体系。

## 版本

- 应用名称：Career Harbor
- 当前版本：0.1.6
- 交付方式：Windows x64 便携 ZIP、macOS Tauri Bundle、Android APK
- 运行方式：解压后直接运行 `Career Harbor.exe`

## 功能

- 简历工作台、模板库、简历编辑器
- 主流招聘网站职位获取、职位线索保存和 JD 导入
- 本地简历存储和自动保存
- JSON、Markdown、PDF、图片导入
- PDF、PNG、Word 等导出能力
- AI 简历生成、优化、JD 匹配分析、求职信、翻译润色
- 模拟面试与面试报告
- 中英双语界面

## 桌面端特性

- 默认本地使用，无登录流程。
- 自定义标题栏，不使用系统原生标题栏。
- 应用图标、窗口标题、包名和运行标识统一为 Career Harbor。
- 采用侧边栏工作台布局，模板库使用列表加预览结构。
- 支持依托 GitHub Releases 的自动更新。

## 开发环境

- Node.js 20.19+ 或 22.12+
- pnpm 9+
- Rust stable
- Windows 桌面构建工具链
- macOS 构建需要 macOS runner 或本机 Xcode Command Line Tools
- Android Studio / Android SDK（Android 本地构建）
- macOS + Xcode（iOS 本地构建）

安装依赖：

```bash
pnpm install
```

启动桌面开发环境：

```bash
pnpm dev:tauri
```

构建桌面前端：

```bash
pnpm build:desktop-shell
```

构建 Tauri 桌面应用：

```bash
pnpm build:tauri
```

构建 macOS Tauri 包需要在 macOS 环境运行：

```bash
pnpm build:tauri:macos
```

移动端开发：

```bash
pnpm dev:mobile
pnpm check:mobile
pnpm build:mobile:android
```

## 项目结构

- `desktop/`：Tauri 前端和 Rust 后端
- `mobile/`：React Native / Expo 移动端 App，复用共享 schema/core/design-tokens 包
- `packages/`：跨端共享 schema、core、design tokens 和可复用 UI 模块
- `src/`：共享 UI、简历模板、类型、导出和 AI 工具代码
- `public/`：共享公开资源
- `drizzle/`：数据库迁移脚本和快照
- `messages/`：多语言文案资源
- `desktop/public/`：桌面端公开资源
- `desktop/src-tauri/icons/`：Tauri 应用图标资源
- `scripts/`：构建、版本同步和发布辅助脚本
- `docs/`：技术文档
- `dist-release/`：本地生成的交付包，默认不提交到 Git

更完整的跨端职责边界见 `docs/PROJECT_STRUCTURE.zh-CN.md`。

## CLI

项目包含一个面向自动化和 agent 的命令行入口：

```bash
cargo build --manifest-path desktop/src-tauri/Cargo.toml --bin job_tool
career-harbor-cli ping
career-harbor-cli resume list
career-harbor-cli resume get <id>
career-harbor-cli resume upsert --file resume.json
```

CLI 默认输出 JSON，并读写桌面 App 的同一个本地工作区。发布 ZIP 会包含 `Career Harbor.exe`、`career-harbor-cli.exe` 和内部更新 helper `career-harbor-updater.exe`，不会暴露旧的 `job-tool.exe`。简历读写命令需要用户激活后获得 `cli` 功能授权。桌面端工作台和编辑器提供刷新按钮，用于同步 agent 通过 CLI 写入的数据。

## 文档

- `docs/DELIVERY.md`：交付包说明
- `docs/PROJECT_STRUCTURE.zh-CN.md`：项目结构、共享套件和桌面/移动端职责边界
- `docs/CLI.md`：命令行入口说明
- `docs/GITHUB_UPLOAD.md`：GitHub 上传说明
- `docs/FEATURE-IDEAS.md`：产品规划与功能池
- `docs/README.md`：文档索引
- `CHANGELOG.md`：版本变更记录
- `AGENTS.md`：开发维护注意事项
