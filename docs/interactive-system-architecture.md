# 即時互動直播系統架構

## 目標

觀眾在 TikTok 聊天室輸入訊息 → 系統偵測關鍵詞 → 虛擬女友 APP 做出對應反應（動作/回話）

---

## 系統架構圖

```
TikTok 直播聊天室
      ↓ TikTokLive Python 套件即時監聽
  關鍵詞偵測腳本（本地 Python）
      ↓ 匹配關鍵詞表 或 送 Claude API 理解語意
  APP 控制層
      ↓ API 指令 / 模擬操作（pyautogui）
  虛擬女友 APP（動作/語音/文字回應）
      ↓ OBS 捕捉畫面
  TikTok 觀眾即時看到反應
```

---

## 技術層說明

### 層一：聊天室監聽

工具：[TikTokLive](https://github.com/isaackogan/TikTokLive)（Python，無需官方 API）

```python
from TikTokLive import TikTokLiveClient
from TikTokLive.events import CommentEvent

client = TikTokLiveClient(unique_id="@你的TikTok帳號")

@client.on(CommentEvent)
async def on_comment(event: CommentEvent):
    keyword_handler(event.user.nickname, event.comment)

client.run()
```

### 層二：關鍵詞對應表（MVP 階段）

| 觸發關鍵詞 | 對應動作 | 回話文字 |
|-----------|---------|---------|
| 親親、kiss | 播放吻的動畫 | 「人家害羞啦～」 |
| 你好、hi | 打招呼動作 | 「你終於來了！」 |
| 我愛你、愛你 | 心心動畫 | 「我也愛你喔♡」 |
| 禮物 | 驚喜表情 | 「哇！謝謝你～」 |
| 晚安 | 揮手動作 | 「要早點睡喔，我會想你的」 |

> MVP 階段用固定關鍵詞表。驗證流程後升級為 Claude API 語意理解，支援任意自然語言輸入。

### 層三：APP 控制方式（依 APP 能力決定）

**優先選擇：有 API 的 APP**
```python
import requests
# 送指令給 APP 的 API
requests.post("http://localhost:PORT/action", json={"action": "kiss"})
```

**備選：模擬鍵盤/滑鼠操作**
```python
import pyautogui
pyautogui.hotkey('ctrl', '1')  # 觸發 APP 設定的快捷鍵動作
```

---

## 開發里程碑

| 階段 | 目標 | 依賴 |
|------|------|------|
| **M1** | Hanburger 確認 APP 外部控制方式 | APP 選型完成 |
| **M2** | TikTokLive 監聽腳本跑起來 | TikTok 帳號直播權限 |
| **M3** | 5 個關鍵詞觸發 APP 動作 | M1 + M2 |
| **M4** | OBS 畫面同步顯示反應 | M3 |
| **M5** | 接入 Claude API 支援自然語言 | M3 驗證成功 |

---

## 關鍵風險

| 風險 | 說明 | 應對 |
|------|------|------|
| APP 無外部控制能力 | 無 API 也無快捷鍵 | 換 APP，或考慮 VTube Studio 自製形象 |
| TikTok 封鎖自動化工具 | TikTokLive 套件可能失效 | 備選 StreamElements / 第三方彈幕工具 |
| 延遲過高 | 訊息→反應超過 3 秒觀眾感受差 | 優先本地處理，Claude API 僅做補充 |
