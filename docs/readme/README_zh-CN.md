<div align="center">

<a href="https://blog.dei3c.com" target="_blank" rel="noopener noreferrer">
  <img src="https://github.com/user-attachments/assets/2830eb70-512c-4ddb-87ec-5213a6e465b1" alt="得翼科技 | Autodesk CAD Suite Assistant" height="70" />
</a>

<br /><br />

[繁体中文](../../README.md) · **简体中文** · [English](README_en.md)

# Autodesk 原生环境诊断与安全修复助手

### AutoCAD、Revit、Inventor、Maya、3ds Max 安装与启动环境问题 · 先预览、再确认、可还原

[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011-blue?style=flat-square)](https://github.com/robert820/autodesk-cad-suite-assistant)
[![License](https://img.shields.io/badge/License-Freeware-informational?style=flat-square)](../../LICENSE)
[![Status](https://img.shields.io/badge/Status-In%20Development-orange?style=flat-square)](#-目前状态)

</div>

---

## 📖 软件简介

协助排查 AutoCAD、Revit、Inventor、Maya 与 3ds Max 无法安装，或安装后无法启动／授权的环境问题。安装前与安装后均可运行唯读扫描；任何变更都需经修复计划预览与明确确认。

**「Autodesk 原生环境诊断与安全修复助手」** 皆采原生 Windows API／COM／WMI／SCM，运行期不依赖外部 CLI 工具。

---

## 📌 目前状态

> 开发中（0.1.0）。已实作唯读扫描与「预览→确认→备份→验证→可还原」的修复框架；**真实系统设置修改仅在可还原的虚拟机中验收**，各版本 Windows 实机验收仍在进行，尚未发布可下载的运行档。

---

## ✨ 功能介绍

### 1. 🔎 产品、MSI 与文件版本侦测
- 读取 HKLM／HKCU 卸载登录（32／64 比特查看）、Autodesk MSI 产品纪录与主程序文件版本；支持自订路径搜索，并以脱机 Authenticode 签章检查安装器候选（不代表安装成功或来源可信）。

### 2. 🩺 环境诊断来源
- 唯读查看 ProgramData／AppData 目录、Autodesk Licensing 与指定服务状态、IFEO 设置、Windows 事件记录（MSI 11708 与已知崩溃事件）、Defender 偏好设置与 Windows 防火墙规则；仅标示供人工审阅。

### 3. 🛡️ 安全修复与还原
- 修复计划仅列出有证据支持的最小项目，缺省全部不勾选；不创建 Allow 规则、不开端口、不加广泛 Defender 排除、不删 IFEO、不停用指定服务。

### 4. 🔐 同意闸门与备份
- GUI 确认对话框与 CLI `--select`／`--confirm`；提权时以 UAC 重新启动同一支已验证运行档；写入前备份、写后重读验证，还原前侦测外部漂移，已被外部程序覆写时停止覆写并标记冲突。

### 5. 🌏 多语、主题与 DPI
- 繁体中文／简体中文／英文动态切换，浅色／深色／跟随系统主题，Per-Monitor V2 DPI 感知，无额外运行库相依。

### 6. ⌨️ 命令行
- 提供 `--scan`、`--dry-run`、`--plan`、`--list-backups`、`--apply`、`--restore` 与 `--help`，并可输出 `--json`。

---

## 💻 支持范围与限制

| 项目 | 目前状态 | 说明 |
| :--- | :--- | :--- |
| AutoCAD／Revit／Inventor／Maya／3ds Max | 诊断范围 | 唯读扫描与诊断涵盖范围；各产品逐版本验收尚未完成 |
| 修复与还原 | 已实作（需确认） | 须预览、明确确认、备份与写后验证；缺省不勾选任何项目 |
| 真实系统修改验收 | 仅限可还原 VM | 开发主机仅运行唯读扫描与仿真后端测试 |
| Windows 版本 | 目标 Windows 10／11 | 建置目标含 Windows 7 兼容层，但建置成功不代表运行兼容已验证 |

---

## 🚀 使用流程

1. 在安装前或安装后启动 GUI（或 CLI `--scan`），运行唯读扫描并查看诊断结果。
2. 如需修复，先产生并预览修复计划（CLI：`--plan`），逐项勾选需要的项目。
3. 明确确认后才套用；程序会先备份、套用后重读验证。需要时可用备份档还原（CLI：`--restore`）。
4. 结果仅是环境线索，并非所有 Autodesk 问题的最终判定。

---

## 📦 下载与使用说明

目前尚未发布可下载的运行档；发布后将提供于本项目的 [Releases 页面](https://github.com/robert820/autodesk-cad-suite-assistant/releases)。

---

## 🖥️ 系统与环境需求

- **操作系统**：Windows 10 / 11
- **运行权限**：唯读扫描无需修改系统；套用修复时才会通过 UAC 提权
- **运行环境**：原生 Rust 运行档，无须额外安装 .NET 或 VC++ 可转发套件

---

## ❓ 常见问题 (FAQ)

<details>
<summary><b>扫描时会更动我的系统吗？</b></summary>

不会。扫描为唯读；任何修复都需先预览并明确确认。

</details>

<details>
<summary><b>这个工具可以保证修好 AutoCAD 或 Revit 吗？</b></summary>

不能。工具仅针对有证据支持的环境问题提供最小修复项目，结果仍需您自行确认。

</details>

<details>
<summary><b>支持哪些 Autodesk 产品？</b></summary>

以 AutoCAD、Revit、Inventor、Maya 与 3ds Max 为诊断范围；各产品逐版本验收尚未完成，请以后续版本说明为准。

</details>

---

## 💬 问题反馈与支持

- 🐛 **错误回报与功能建议**：欢迎至本项目的 [Issues 页面](https://github.com/robert820/autodesk-cad-suite-assistant/issues) 提出。
- 🌐 **得翼科技官方网站**：[https://blog.dei3c.com](https://blog.dei3c.com)
- 📧 **技术支持与商务洽询**：请通过官方网站联系我们。

---

## 📄 授权条款 (License)

本软件采用专有免费软件授权（Proprietary Freeware），完整授权规范、使用条款与免责声明请参阅 [LICENSE](../../LICENSE) 文件。

- 第三方组件：本软件使用 Slint（Royalty-Free License）、YY-Thunks（MIT）与多个开源 Rust 套件，授权声明请见 [THIRD_PARTY_NOTICES.md](../../THIRD_PARTY_NOTICES.md)。

<a href="https://slint.dev"><picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/slint-ui/slint/master/logo/MadeWithSlint-logo-dark.png">
  <img src="https://raw.githubusercontent.com/slint-ui/slint/master/logo/MadeWithSlint-logo-light.png" alt="Made with Slint" width="160">
</picture></a>
