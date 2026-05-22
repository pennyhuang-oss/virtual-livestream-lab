# Vincent 任務 01：生成虛擬女主播角色形象

**負責人：** Vincent  
**目標：** 產出一組可用於 HeyGen 訓練的虛擬女主播素材  
**驗收：** Penny 選臉確認後，進入 Step 2 影片生成  

---

## 角色設定

- **風格：** 娛樂型女主播，可唱歌跳舞，居家感、不正式
- **氣質：** 鄰家女孩感，親切討喜，不是模特那種冰冷完美
- **真實度要求：** 看到第一眼以為是真人，30 秒後才開始懷疑

---

## Step 1｜Midjourney 生成基礎角色

### 主 Prompt（直接複製使用）

```
photorealistic young asian woman, 22-25 years old, casual homewear, 
warm cozy bedroom background with soft lamp light, 
natural beauty with subtle imperfections, skin pores visible, 
slight natural asymmetry in face, soft under-eye shadow, 
flyaway hair, natural hairline, loose wavy hair, 
warm smile, approachable and friendly expression, 
single window light from left side, soft shadows, 
slight depth of field blur on background, 
shot on iPhone, slight grain, candid feel,
--ar 9:16 --style raw --v 7
```

### 多角度生成（保持同一張臉）

第一張滿意後，用 `--cref [第一張圖URL]` 生成以下角度，每個角度各 3 張：

```
# 正臉
same woman, facing camera directly, neutral expression, soft smile
--cref [URL] --cw 80 --ar 9:16 --style raw --v 7

# 左側 45 度
same woman, 3/4 left angle, slightly looking at camera, candid
--cref [URL] --cw 80 --ar 9:16 --style raw --v 7

# 右側 45 度  
same woman, 3/4 right angle, laughing naturally, eyes crinkled
--cref [URL] --cw 80 --ar 9:16 --style raw --v 7

# 低頭看手機
same woman, looking down at phone, soft smile, cozy vibe
--cref [URL] --cw 80 --ar 9:16 --style raw --v 7

# 唱歌表情
same woman, mouth slightly open singing, eyes bright, joyful
--cref [URL] --cw 80 --ar 9:16 --style raw --v 7
```

### Negative Prompt（必加）

```
perfect skin, airbrushed, plastic skin, symmetrical face, 
model pose, studio lighting, white background, green screen,
anime, illustration, 3D render, CGI, watermark, text,
heavy makeup, dramatic lighting, professional photoshoot feel
```

---

## Step 2｜ComfyUI + IP-Adapter 鎖臉（選出最好的一張後做）

從 Step 1 選出 Penny 確認的臉，用 IP-Adapter 批量生成更多表情：

**IP-Adapter 強度設定：0.85**（高一致性，臉不漂移）

需要生成的表情清單：
- [ ] 微笑（嘴角上揚，眼睛有神）
- [ ] 大笑（自然，不誇張）
- [ ] 害羞（微微低頭，眼神往上看）
- [ ] 驚訝（嘴微開，眼睛放大）
- [ ] 唱歌（嘴型張開，投入感）
- [ ] 無表情待機（自然放鬆，不呆滯）

---

## Step 3｜Kling 2.0 生成訓練影片（15-30 秒）

圖片確認後，用 Kling 2.0 讓角色動起來。

### 影片 Prompt

```
young asian woman in cozy bedroom, sitting casually, 
natural breathing motion, slight head movement, 
looking at camera warmly, blinking naturally, 
soft smile, hair moving slightly from air,
candid home livestream feel, shot on phone camera,
slight handheld shake, warm lamp light, film grain
```

### 技術設定

| 項目 | 設定 |
|------|------|
| 時長 | 15-30 秒 |
| 動作幅度 | 小（只要有自然呼吸和頭部微動即可） |
| 鏡頭 | 固定，輕微手持感 |
| 不需要 | 誇張動作、舞蹈（訓練用，越自然越好）|

> **重點：** 這段影片是給 HeyGen 訓練用的，目的是捕捉臉部特徵，不是展示才藝。讓她自然地看著鏡頭說幾句話或微笑就夠。

---

## 驗收標準（Penny + 謝景行 審核）

- [ ] 第一眼看不出是 AI 生成
- [ ] 皮膚有質感，不像塑料
- [ ] 臉在不同角度保持一致（同一個人）
- [ ] 表情自然，不像貼圖
- [ ] 影片裡的晃動和眨眼感覺真實
- [ ] 整體氣質符合「居家感娛樂主播」

---

## 產出清單

```
/assets/
  character-ref-main.jpg      ← 主要參考臉（Penny 選定）
  character-front.jpg
  character-left45.jpg
  character-right45.jpg
  character-laugh.jpg
  character-shy.jpg
  character-singing.jpg
  training-video-15s.mp4      ← 給 HeyGen 訓練用
```
