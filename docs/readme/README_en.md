<div align="center">

<a href="https://blog.dei3c.com" target="_blank" rel="noopener noreferrer">
  <img src="https://github.com/user-attachments/assets/2830eb70-512c-4ddb-87ec-5213a6e465b1" alt="得翼科技 | Autodesk CAD Suite Assistant" height="70" />
</a>

<br /><br />

[繁體中文](../../README.md) · [简体中文](README_zh-CN.md) · **English**

# Autodesk CAD Suite Assistant

### Diagnose and safely repair install / launch / licensing environment issues of Autodesk products

[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011-blue?style=flat-square)](https://github.com/robert820/autodesk-cad-suite-assistant)
[![License](https://img.shields.io/badge/License-Freeware-informational?style=flat-square)](../../LICENSE)
[![Status](https://img.shields.io/badge/Status-In%20Development-orange?style=flat-square)](#-current-status)

</div>

---

## 📖 Overview

Helps investigate environment problems that stop AutoCAD, Revit, Inventor, Maya and 3ds Max from installing, or from launching / licensing after installation. A read-only scan can be run before and after installation; every change requires a repair-plan preview and explicit confirmation.

**Autodesk CAD Suite Assistant** uses native Windows APIs / COM / WMI / SCM only; it does not depend on external CLI tools at runtime.

---

## 📌 Current status

> In development (0.1.0). Read-only scanning and a preview → confirm → backup → verify → restorable repair framework are implemented; **real system-setting changes are only validated inside revertible virtual machines**, per-version Windows validation is still ongoing, and no downloadable build has been released yet.

---

## ✨ Features

### 1. 🔎 Product, MSI and file-version detection
- Reads HKLM / HKCU uninstall entries (32/64-bit views), Autodesk MSI product records and main-executable file versions; supports custom path search and an offline Authenticode check of installer candidates (which does not prove a successful or trustworthy install).

### 2. 🩺 Diagnostic sources
- Read-only inspection of ProgramData / AppData folders, Autodesk Licensing and designated service states, IFEO settings, Windows event logs (MSI 11708 and known crash events), Defender preferences and Windows Firewall rules; findings are flagged for manual review only.

### 3. 🛡️ Safe repair and restore
- The repair plan lists only minimal, evidence-backed items, all unselected by default; it creates no Allow rules, opens no ports, adds no broad Defender exclusions, deletes no IFEO entries and stops no designated services.

### 4. 🔐 Consent gate and backups
- GUI confirmation dialog and CLI `--select` / `--confirm`; elevation relaunches the same verified executable through UAC; backup before writing, read-back verification after writing, and drift detection before restore, which stops and flags a conflict if something else has overwritten the setting.

### 5. 🌏 Languages, themes and DPI
- Live Traditional Chinese / Simplified Chinese / English switching, light / dark / follow-system themes, Per-Monitor V2 DPI awareness, no extra runtime dependencies.

### 6. ⌨️ Command line
- Provides `--scan`, `--dry-run`, `--plan`, `--list-backups`, `--apply`, `--restore` and `--help`, with optional `--json` output.

---

## 💻 Scope & limitations

| Item | Status | Notes |
| :--- | :--- | :--- |
| AutoCAD / Revit / Inventor / Maya / 3ds Max | Diagnostic scope | Scope of the read-only scan and diagnostics; per-product, per-version validation is not complete |
| Repair & restore | Implemented (needs confirmation) | Requires preview, explicit confirmation, backup and read-back verification; nothing is selected by default |
| Real-system change validation | Revertible VMs only | The development host runs only read-only scans and mock-backend tests |
| Windows version | Targets Windows 10 / 11 | The build includes a Windows 7 compatibility layer, but a successful build does not prove runtime compatibility |

---

## 🚀 Workflow

1. Launch the GUI (or CLI `--scan`) before or after installation and run the read-only scan.
2. If repair is needed, generate and preview the repair plan (CLI: `--plan`) and tick only the items you want.
3. Apply only after explicit confirmation; the app backs up first and verifies by reading back. Restore from a backup when needed (CLI: `--restore`).
4. The results are environmental leads, not a final verdict on every Autodesk problem.

---

## 📦 Download

No downloadable build has been released yet. Once released, it will be provided on the [Releases page](https://github.com/robert820/autodesk-cad-suite-assistant/releases).

---

## 🖥️ Requirements

- **OS**: Windows 10 / 11 (per-version validation not yet completed)
- **Privileges**: scanning is read-only; UAC elevation happens only when applying repairs
- **Runtime**: native Rust executable; no .NET or VC++ redistributable required

---

## ❓ FAQ

<details>
<summary><b>Does scanning change my system?</b></summary>

No. Scanning is read-only; any repair needs a preview and explicit confirmation first.

</details>

<details>
<summary><b>Can it guarantee a fix for AutoCAD or Revit?</b></summary>

No. It offers only minimal, evidence-backed repair items for environment problems; you must still verify the outcome.

</details>

<details>
<summary><b>Which Autodesk products are covered?</b></summary>

AutoCAD, Revit, Inventor, Maya and 3ds Max are in the diagnostic scope; per-product, per-version validation is not complete, so follow the notes of future versions.

</details>

---

## 💬 Feedback & support

- 🐛 **Bug reports & feature requests**: please use the [Issues page](https://github.com/robert820/autodesk-cad-suite-assistant/issues).
- 🌐 **DEI Tech official website**: [https://blog.dei3c.com](https://blog.dei3c.com)
- 📧 **Support & business inquiries**: please contact us through the official website.

---

## 📄 License

This software is released under a Proprietary Freeware license. See the [LICENSE](../../LICENSE) file for the full terms and disclaimers.

- Third-party components: this software uses Slint (Royalty-Free License), YY-Thunks (MIT) and several open-source Rust crates; see [THIRD_PARTY_NOTICES.md](../../THIRD_PARTY_NOTICES.md) for the notices.

<a href="https://slint.dev"><picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/slint-ui/slint/master/logo/MadeWithSlint-logo-dark.png">
  <img src="https://raw.githubusercontent.com/slint-ui/slint/master/logo/MadeWithSlint-logo-light.png" alt="Made with Slint" width="160">
</picture></a>
