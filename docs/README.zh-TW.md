# Acrool Desktop App

[文件入口](../README.md) | 繁體中文 | [English](README.en.md)

Acrool 是一套從軟體開發者視角設計的雲端任務管理平台，協助團隊在同一個工作區管理任務、專案、團隊協作、狀態流程與交付進度。

## 目錄

- [產品介紹](#產品介紹)
- [功能與特性](#功能與特性)
- [下載 Acrool App](#下載-acrool-app)
- [MCP 連線](#mcp-連線)
- [回報問題](#回報問題)
- [相關連結](#相關連結)

## 產品介紹

Acrool 是一套注重使用者體驗的雲端任務管理系統，適合軟體開發、產品、設計與跨職能團隊使用。它以開發者的工作流程為核心，將任務、專案、團隊、客戶資料、狀態流程與協作紀錄整合在同一個工作區，協助團隊更快掌握工作狀態、分派責任並追蹤交付進度。

## 功能與特性

- **狀態群組任務清單**：依狀態整理任務，快速查看待確認、待測試、進行中、逾期或已標記重要的工作。
- **任務與專案管理**：支援日常維運任務與專案任務，並可管理專案階段、任務狀態、報價、User Stories、設計稿連結與客戶資訊。
- **Gantt 甘特圖**：提供專案甘特圖與人員分配狀態甘特圖，協助團隊掌握時程與資源配置。
- **團隊協作**：可建立團隊、邀請成員、管理 Repository / 專案庫，讓任務具備明確歸屬。
- **RBAC 權限控管**：依團隊或成員設定合適權限，讓協作更安全。
- **狀態控制與協作流程**：支援同步狀態變更，讓多人協作時仍能維持流程一致性。
- **PWA 推播通知**：透過通知提醒任務負責人，減少人工提醒成本。
- **活動紀錄**：追蹤工作區內近期任務變更與操作紀錄，便於回溯工作狀態。
- **快捷鍵操作**：支援列表、Markdown 編輯器、下拉選單與彈窗等場景的快捷鍵，提升任務編輯效率。
- **多語系介面**：可依使用者習慣切換介面語言。

## 下載 Acrool App

請至 [Releases](https://github.com/acrool/acrool/releases) 下載最新版本的 Acrool Desktop App。

macOS 安裝後若出現「檔案已損毀，無法打開」或 Gatekeeper 相關提示，可在終端機執行：

```bash
xattr -cr /Applications/Acrool.app
```

參考：[解決 macOS Ventura 13 檔案已損毀無法打開技巧方法](https://medium.com/@imaginechiu/%E8%A7%A3%E6%B1%BAmacos-ventura-13-%E6%AA%94%E6%A1%88%E5%B7%B2%E6%90%8D%E6%AF%80%E7%84%A1%E6%B3%95%E6%89%93%E9%96%8B%E6%8A%80%E5%B7%A7%E6%96%B9%E6%B3%95-2aa4f28e181e)

## MCP 連線

Acrool 提供 MCP（Model Context Protocol）連線，讓 Claude Desktop、Claude Code (CLI)、OpenAI Codex CLI 等 AI 助理可以直接在對話中讀取與更新你的任務。

詳細設定步驟請參考：[連接 Acrool 到 Claude / AI（MCP）](connect-claude-mcp.zh-TW.md)。

## 回報問題

如果在使用 Acrool App 時遇到錯誤，請至 [Issues](https://github.com/acrool/acrool/issues) 建立回報，並盡量提供：

- 作業系統與版本
- Acrool App 版本
- 問題發生步驟
- 預期結果與實際結果
- 截圖、錄影或錯誤訊息

## 相關連結

- 官網：[acrool.com](https://acrool.com/)
- 文件：[docs.acrool.com](https://docs.acrool.com/)
- 更新紀錄：[docs.acrool.com/changelog](https://docs.acrool.com/changelog)
