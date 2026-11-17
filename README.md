<div align="center">

<a href="https://blog.dei3c.com" target="_blank" rel="noopener noreferrer">
  <img src="https://github.com/user-attachments/assets/2830eb70-512c-4ddb-87ec-5213a6e465b1" alt="得翼科技 | Autodesk CAD Suite Assistant" height="70" />
</a>

<br /><br />

**繁體中文** · [简体中文](docs/readme/README_zh-CN.md) · [English](docs/readme/README_en.md)

# Autodesk 原生環境診斷與安全修復助手

### AutoCAD、Revit、Inventor、Maya、3ds Max 安裝與啟動環境問題 · 先預覽、再確認、可還原

[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011-blue?style=flat-square)](https://github.com/robert820/autodesk-cad-suite-assistant)
[![License](https://img.shields.io/badge/License-Freeware-informational?style=flat-square)](LICENSE)
[![Status](https://img.shields.io/badge/Status-In%20Development-orange?style=flat-square)](#-目前狀態)

</div>

---

## 📖 軟體簡介

協助排查 AutoCAD、Revit、Inventor、Maya 與 3ds Max 無法安裝，或安裝後無法啟動／授權的環境問題。安裝前與安裝後均可執行唯讀掃描；任何變更都需經修復計畫預覽與明確確認。

**「Autodesk 原生環境診斷與安全修復助手」** 皆採原生 Windows API／COM／WMI／SCM，執行期不依賴外部 CLI 工具。

---

## 📌 目前狀態

> 開發中（0.1.0）。已實作唯讀掃描與「預覽→確認→備份→驗證→可還原」的修復框架；**真實系統設定修改僅在可還原的虛擬機中驗收**，各版本 Windows 實機驗收仍在進行，尚未發布可下載的執行檔。

---

## ✨ 功能介紹

### 1. 🔎 產品、MSI 與檔案版本偵測
- 讀取 HKLM／HKCU 解除安裝登錄（32／64 位元檢視）、Autodesk MSI 產品紀錄與主程式檔案版本；支援自訂路徑搜尋，並以離線 Authenticode 簽章檢查安裝器候選（不代表安裝成功或來源可信）。

### 2. 🩺 環境診斷來源
- 唯讀檢視 ProgramData／AppData 目錄、Autodesk Licensing 與指定服務狀態、IFEO 設定、Windows 事件記錄（MSI 11708 與已知崩潰事件）、Defender 偏好設定與 Windows 防火牆規則；僅標示供人工審閱。

### 3. 🛡️ 安全修復與還原
- 修復計畫僅列出有證據支持的最小項目，預設全部不勾選；不建立 Allow 規則、不開埠、不加廣泛 Defender 排除、不刪 IFEO、不停用指定服務。

### 4. 🔐 同意閘門與備份
- GUI 確認對話框與 CLI `--select`／`--confirm`；提權時以 UAC 重新啟動同一支已驗證執行檔；寫入前備份、寫後重讀驗證，還原前偵測外部漂移，已被外部程式覆寫時停止覆寫並標記衝突。

### 5. 🌏 多語、主題與 DPI
- 繁體中文／簡體中文／英文動態切換，淺色／深色／跟隨系統主題，Per-Monitor V2 DPI 感知，無額外執行庫相依。

### 6. ⌨️ 命令列
- 提供 `--scan`、`--dry-run`、`--plan`、`--list-backups`、`--apply`、`--restore` 與 `--help`，並可輸出 `--json`。

---

## 💻 支援範圍與限制

| 項目 | 目前狀態 | 說明 |
| :--- | :--- | :--- |
| AutoCAD／Revit／Inventor／Maya／3ds Max | 診斷範圍 | 唯讀掃描與診斷涵蓋範圍；各產品逐版本驗收尚未完成 |
| 修復與還原 | 已實作（需確認） | 須預覽、明確確認、備份與寫後驗證；預設不勾選任何項目 |
| 真實系統修改驗收 | 僅限可還原 VM | 開發主機僅執行唯讀掃描與模擬後端測試 |
| Windows 版本 | 目標 Windows 10／11 | 建置目標含 Windows 7 相容層，但建置成功不代表執行相容已驗證 |

---

## 🚀 使用流程

1. 在安裝前或安裝後啟動 GUI（或 CLI `--scan`），執行唯讀掃描並檢視診斷結果。
2. 如需修復，先產生並預覽修復計畫（CLI：`--plan`），逐項勾選需要的項目。
3. 明確確認後才套用；程式會先備份、套用後重讀驗證。需要時可用備份檔還原（CLI：`--restore`）。
4. 結果僅是環境線索，並非所有 Autodesk 問題的最終判定。

---

## 📦 下載與使用說明

目前尚未發布可下載的執行檔；發布後將提供於本專案的 [Releases 頁面](https://github.com/robert820/autodesk-cad-suite-assistant/releases)。

---

## 🖥️ 系統與環境需求

- **作業系統**：Windows 10 / 11
- **執行權限**：唯讀掃描無需修改系統；套用修復時才會透過 UAC 提權
- **執行環境**：原生 Rust 執行檔，無須額外安裝 .NET 或 VC++ 可轉發套件

---

## ❓ 常見問題 (FAQ)

<details>
<summary><b>掃描時會更動我的系統嗎？</b></summary>

不會。掃描為唯讀；任何修復都需先預覽並明確確認。

</details>

<details>
<summary><b>這個工具可以保證修好 AutoCAD 或 Revit 嗎？</b></summary>

不能。工具僅針對有證據支持的環境問題提供最小修復項目，結果仍需您自行確認。

</details>

<details>
<summary><b>支援哪些 Autodesk 產品？</b></summary>

以 AutoCAD、Revit、Inventor、Maya 與 3ds Max 為診斷範圍；各產品逐版本驗收尚未完成，請以後續版本說明為準。

</details>

---

## 💬 問題反饋與支援

- 🐛 **錯誤回報與功能建議**：歡迎至本專案的 [Issues 頁面](https://github.com/robert820/autodesk-cad-suite-assistant/issues) 提出。
- 🌐 **得翼科技官方網站**：[https://blog.dei3c.com](https://blog.dei3c.com)
- 📧 **技術支援與商務洽詢**：請透過官方網站聯繫我們。

---

## 📄 授權條款 (License)

本軟體採用專有免費軟體授權（Proprietary Freeware），完整授權規範、使用條款與免責聲明請參閱 [LICENSE](LICENSE) 檔案。

- 第三方元件：本軟體使用 Slint（Royalty-Free License）、YY-Thunks（MIT）與多個開源 Rust 套件，授權聲明請見 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

<a href="https://slint.dev"><picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/slint-ui/slint/master/logo/MadeWithSlint-logo-dark.png">
  <img src="https://raw.githubusercontent.com/slint-ui/slint/master/logo/MadeWithSlint-logo-light.png" alt="Made with Slint" width="160">
</picture></a>
