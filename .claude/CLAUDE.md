# Virtual Livestream Lab — 專案指引

## 專案背景

本專案目標是搭建一套「AI 虛擬人直播間」解決方案，能因應不同客戶需求（虛擬女友、帶貨、教學、娛樂等）。
首期測試以「虛擬女友 APP 直播間」為場景，使用 OBS + TikTok Live Studio 驗證基本架構。

## 當前優先任務

1. Hanburger 蒐集並評估適合測試的虛擬女友 APP
2. 建立 OBS + TikTok Live Studio 的直播投影流程
3. 確認直播間互動腳本基本框架

## 團隊與分工

### 真實成員
- **Penny**（`penny-director.md`）：專案負責人，整體決策
- **Hanburger**（`hanburger-intern.md`）：APP 測試評估，由 Penny 直接管理
- **Vincent**（`vincent-aigc.md`）：AIGC 技術指導，後期虛擬形象製作

### 虛擬策略顧問
- **時宴**（`shiyan-strategist.md`）：商業判斷、專案方向把關
- **宋潛機**（`songqianji-ops.md`）：成本控制、流程優化、MVP 建議
- **冉方旭**（`ranfangxu-script.md`）：腳本研究、深度內容、問題診斷
- **許七安**（`xuqian-content.md`）：企劃設計、觀眾溝通、內容轉譯
- **謝景行**（`xiejingxing-qa.md`）：QA 審核、風險把關、上線前終審

## 工作流程

```
時宴 評估方向是否值得做
  ↓
宋潛機 設計最小可行版本
  ↓
冉方旭 研究內容 + 撰寫腳本
  ↓
許七安 轉成觀眾看得懂的語言
  ↓
謝景行 最終審核，砍廢話、看風險
  ↓
Penny 決策上線
```

## 指令說明

- `/find-vgf-app` — 評估虛擬女友 APP 適配性
- `/create-script` — 產生直播腳本
- `/stream-checklist` — 直播前設備檢查清單
