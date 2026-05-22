# OBS + TikTok Live Studio 直播投影設定指南

## 架構說明

```
虛擬女友 APP（手機/電腦）
        ↓ 畫面捕捉
       OBS
        ↓ 推流
TikTok Live Studio → TikTok 直播
```

## 方案一：電腦 APP 直接捕捉（最簡單）

APP 若有 PC 版（如 Replika Web、Character.AI 等），直接用 OBS 的「視窗捕捉」：
1. OBS → 新增來源 → 視窗捕捉 → 選擇 APP 視窗
2. 調整 9:16 比例（TikTok 豎版）
3. OBS → 工具 → VirtualCam → 啟動

## 方案二：手機畫面投影到電腦

需要手機投影工具：
- **iOS**：QuickTime Player（USB 連接）或 Reflector 4
- **Android**：scrcpy（免費開源）或 AirDroid Cast

步驟：
1. 手機畫面投影到電腦後，OBS 捕捉投影視窗
2. 其餘步驟同方案一

## TikTok Live Studio 設定

1. 下載安裝 [TikTok Live Studio](https://www.tiktok.com/live/creators/live-studio/)
2. 登入 TikTok 帳號
3. 進入「設定」→「串流設定」→ 取得推流金鑰
4. OBS 設定：
   - 設定 → 串流 → 服務選「自訂」
   - 伺服器：`rtmp://push.tiktokv.com/live/`
   - 串流金鑰：從 TikTok Live Studio 取得

## 推薦 OBS 輸出設定

| 項目 | 設定值 |
|------|------|
| 解析度 | 1080 × 1920（9:16） |
| 幀率 | 30 fps |
| 編碼器 | x264 或硬體加速 |
| 位元率 | 4500~6000 kbps |
| 音頻位元率 | 128 kbps |

## 注意事項

- TikTok 直播需帳號達一定粉絲數（各地區要求不同）
- 直播中途避免切換 APP，防止畫面黑屏
- 建議開啟 OBS 本地錄影備份
