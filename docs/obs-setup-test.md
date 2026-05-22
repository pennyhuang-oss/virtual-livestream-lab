# OBS 直播場景設定測試記錄

OBS 版本：32.1.2 | 系統：macOS | 螢幕：4K + Retina

## 測試目標

用 OBS 捕捉虛擬女友 APP 畫面，以 9:16 豎版格式推流至 TikTok Live Studio。

---

## Step 1：建立 9:16 豎版畫布

OBS → 設定（Settings）→ 影像（Video）：

| 項目 | 設定值 |
|------|------|
| Base (Canvas) Resolution | 1080 × 1920 |
| Output (Scaled) Resolution | 1080 × 1920 |
| Downscale Filter | Lanczos |
| FPS | 30 |

> 注意：macOS Retina 螢幕預設是 2x，OBS 會自動處理，不需要設 2160×3840。

## Step 2：建立場景與來源

新增場景：`虛擬直播-測試`

來源（Sources）優先順序（由上到下）：

```
1. 麥克風音訊（Audio Input Capture）
2. APP 視窗（Window Capture 或 Display Capture）
3. 背景（Color Source 黑色，填滿 1080×1920）
```

## Step 3：APP 畫面捕捉方式

### 方案 A：電腦版 APP（直接捕捉）
- 來源 → 視窗捕捉（Window Capture）
- 選擇對應的 APP 視窗
- 勾選「捕捉音訊」（若需要 APP 音效）

### 方案 B：手機畫面投影
- iPhone：用 QuickTime Player（USB 線）→ 檔案 → 新增影片收錄 → 選手機
- Android：安裝 scrcpy，執行後 OBS 捕捉 scrcpy 視窗
- 捕捉後同方案 A

## Step 4：音頻設定

OBS → 音訊混音器（Audio Mixer）：
- 麥克風電平目標：-12dB ~ -6dB（說話時）
- APP 音效：視需求開關，直播時建議靜音（用人聲主導）

## Step 5：推流設定（串接 TikTok Live Studio）

**選項一：透過 TikTok Live Studio 內建捕捉**
直接在 TikTok Live Studio 中新增「Window Capture」來源，不需要 OBS。

**選項二：OBS 推流至 TikTok（進階）**
OBS → 設定 → 串流：
- 服務：自訂
- 伺服器：`rtmp://push.tiktokv.com/live/`
- 串流金鑰：從 TikTok Live Studio 取得

**選項三：OBS Virtual Camera → TikTok Live Studio（推薦測試用）**
1. OBS → 工具 → VirtualCam → 啟動虛擬攝影機
2. 開啟 TikTok Live Studio
3. 攝影機來源選「OBS Virtual Camera」
4. 這樣可以保留 OBS 的場景彈性，同時用 TikTok Live Studio 管理直播

---

## 測試記錄

| 日期 | 測試項目 | 結果 | 備註 |
|------|---------|------|------|
| | 9:16 畫布建立 | | |
| | APP 畫面捕捉 | | |
| | 麥克風電平 | | |
| | VirtualCam 啟動 | | |
| | TikTok 接收畫面 | | |
