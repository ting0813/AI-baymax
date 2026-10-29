# 🎈 AI Baymax Plushie

AI Baymax Plushie 是一個開源的軟硬體改造專案，目標是將市售的 50cm–80cm 絨毛杯麵（Baymax）娃娃，改造成一個具備同理心、語音互動能力與本地邊緣運算能力的 AI 伴侶機器人。

<p align="center">
  <img src="https://github.com/ting0813/AI-plush-giraffe/blob/main/Gemini_Generated_Image_xbjvv3xbjvv3xbjv.jpg?raw=true" alt="AI Baymax Plushie" width="900" />
</p>

本專案結合 Raspberry Pi、大型語言模型（LLM）、語音辨識與硬體互動模組，打造一個能聽、能說、能理解、並以溫暖方式回應的陪伴型智慧玩偶。

---

## ✨ 專案概覽

本專案的目標，是將軟軟的絨毛娃娃轉變成一台真正的 AI 伴侶機器人，具備以下能力：

- 語音喚醒與連續聆聽
- 語音轉文字（STT）
- 具同理心的對話回應（LLM）
- 自然語音輸出（TTS）
- 可選的低溫暖感觸覺（加熱墊）
- 呼吸燈狀態指示
- 溫和的點頭、搖頭、揮手等動作

透過邊緣端與雲端 AI 的混合架構，娃娃可以在本地端快速反應，同時利用雲端模型提供更自然、更智能的對話能力。

---

## 🧠 核心功能

- 🎙️ 喚醒詞偵測
  - 在邊緣端本地運行
  - 低延遲且保護隱私

- 🧠 同理心 LLM 人設
  - 透過客製化 Prompt 讓 AI 以溫和、耐心、關懷的語氣回應
  - 特別適合陪伴式、情緒支持型互動

- 🗣️ 自然語音對話
  - 整合 STT 與 TTS，提供接近真人的對話體驗

- 🔥 物理療癒感
  - 加入低溫加熱墊，模擬擁抱時的暖意

- 💡 呼吸式狀態燈
  - 表示待機、聆聽、思考與說話狀態

- 🤝 安全的機械互動
  - 可透過伺服機實現點頭、搖頭與揮手
  - 所有動作都受安全範圍與限制控制

---

## 🏗️ 系統架構

本專案採用「邊緣端 + 雲端 AI」的混合架構：

- 邊緣端（Raspberry Pi）負責喚醒、音訊處理、狀態燈、以及動作控制
- 雲端節點（LLM / STT / TTS）負責語意理解與自然語音生成

這種架構使娃娃兼具：

- 低延遲反應
- 隱私保護
- 自然對話能力
- 安全可控的物理互動

```text
SMART CUP NOODLES
 ┌────────────────────────────────────────────┐
 │                AMB82-Mini                  │
 │                                            │
 │ Camera ──> local vision ──> perception     │
 │ Mic ─────> audio/event detection           │
 │                                            │
 │            Cup Noodles Agent API           │
 │        HTTP/WebSocket JSON interface       │
 │                    │                       │
 │       ┌────────────┼────────────┐          │
 │       ▼            ▼            ▼          │
 │    Speaker       Servos        LEDs        │
 │   / playback   head / ears   expression    │
 └────────────────────┬───────────────────────┘
                      │ Wi-Fi
                      │
              Android phone/tablet
 ┌────────────────────▼───────────────────────┐
 │          Google AI Edge Gallery            │
 │                                            │
 │        on-device model / agent             │
 │                 │                          │
 │       Cup Noodles Agent Skill              │
 │                 │                          │
 │        JS Skill / MCP ecosystem            │
 │                 │                          │
 │       ┌─────────┼─────────┐                │
 │       ▼         ▼         ▼                │
 │     look()    emotion()   move()           │
 │     status()  play()      etc.             │
 └────────────────────────────────────────────┘
```

這個架構讓娃娃在邊緣端快速反應，同時將語意理解與自然對話交由雲端 AI 完成，整體效果更接近真實的互動型陪伴裝置。

---

## 🧰 硬體需求

1. 絨毛外殼
   - 50cm–80cm 商業化杯麵風格絨毛娃娃

2. 主控板
   - Raspberry Pi 4B（推薦）
   - Raspberry Pi Zero 2 W（小型化版本）

3. 音訊模組
   - USB 麥克風
   - 迷你擴音喇叭 / 喇叭放大模組

4. 電源
   - 10,000mAh 行動電源
   - 建議支援邊充邊放（pass-through charging）

5. 配件
   - 3D 列印保護殼
   - 拉鍊、魔鬼氈、散熱片、絕緣材質

6. 可選模組
   - 低溫加熱墊（約 38°C）
   - 狀態 LED
   - 伺服機（點頭 / 搖頭 / 揮手）

---

## 🛠️ 軟體技術棧

- 作業系統：Raspberry Pi OS / Linux
- 程式語言：Python 3
- 喚醒詞偵測：Porcupine、Snowboy 或類似方案
- 語音辨識：OpenAI Whisper API / 本地端 STT
- 語言模型：GPT-4o、Claude 或開源本地模型
- 文字轉語音：OpenAI TTS、ElevenLabs 或本地端 TTS
- 控制層：Python 服務或本地 Agent 邏輯

---

## 🚀 快速開始

### 1. 複製專案

```bash
git clone https://github.com/yourusername/AI-Baymax-Plushie.git
cd AI-Baymax-Plushie
```

### 2. 建立虛擬環境

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. 安裝依賴套件

```bash
pip install -r requirements.txt
```

### 4. 設定環境變數

建立 `.env` 檔案並填入相關金鑰：

```env
OPENAI_API_KEY=your_openai_api_key
PICOVOICE_API_KEY=your_picovoice_api_key
```

### 5. 啟動桌面概念驗證（PoC）

先不要直接裝進娃娃內，先在桌面環境測試音訊輸入與輸出：

```bash
python main.py
```

---

## ⚠️ 安全警告

本專案涉及將電子元件安裝進棉花與布料材質的絨毛娃娃內部，因此存在明顯的火災、過熱與短路風險。安全設計必須被視為首要條件。

建議遵守以下事項：

- Raspberry Pi、電池和線路必須與棉花素材隔離
- 使用阻燃或耐熱的防護外殼
- 加入散熱孔與適當的散熱設計
- 確保裸露電路板不直接接觸布料或棉花
- 在測試時持續監控溫度
- 使用穩壓與適當電壓供電
- 本專案仍屬原型階段，未完成正式安全測試前請勿直接大量生產

---

## 📦 儲存庫結構

```text
AI-plush-giraffe/
├── README.md
├── ai_readme.md
├── PROPOSAL.md
├── SKILL.md
├── GiraffeAgent.ino
├── assets/
│   ├── plush_toy_giraffe.webp
│   ├── AI-plush-giraffe_architecture_diagram.png
│   └── AI-plush-toy_block_diagram.png
├── scripts/
│   └── index.html
├── .env.example
├── requirements.txt
├── main.py
└── LICENSE
```

---

## 📜 授權說明

本專案僅供教育、研究與原型開發用途。若要實際改造任何消費性產品，請先確認符合當地電子與安全法規要求。

---

## 🤝 貢獻方式

歡迎任何形式的貢獻，包含但不限於：

- 改善語音處理流程
- 修正電路與安裝設計
- 優化 AI Prompt
- 製作可重複使用的 3D 結構
- 補充安全與測試文件

如果你有好點子或想協作實作，歡迎提交 Issue 或 Pull Request。

---

## 🔮 未來發展方向

未來可擴充的方向包括：

- 更強的本地喚醒詞與低延遲處理
- 更自然的中文 / 英文語音互動
- 更安全的伺服機控制與動作界限
- 更細緻的情緒模型與陪伴風格調校
- 更強的邊緣 AI 與本地模型整合
- 最終實現可持續使用的 AI 絨毛伴侶裝置

---

## 致謝

本專案受益於 AI 絨毛玩具、邊緣運算、語音 AI 與智慧家電領域的相關創新思路。若能將這些技術整合成更貼近人類陪伴感的互動裝置，將是一個極具實用價值與未來潛力的創作方向。
