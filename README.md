# 🎈 AI Baymax Plushie (AI 杯麵絨毛機器人)

<p align="center">
  <img src="https://github.com/ting0813/AI-plush-giraffe/blob/main/Gemini_Generated_Image_xbjvv3xbjvv3xbjv.jpg?raw=true" alt="AI Baymax Plushie" width="900" />
</p>

這是一個開源的軟硬體改造專案，目標是將市售的 50cm–80cm 「杯麵 (Baymax)」絨毛娃娃，改造成一台真正能聽、能說、能理解、甚至會用溫暖語氣回應人的 AI 伴侶機器人。

本專案整合 Raspberry Pi、語音處理、語意模型（LLM）與物理互動模組，將電影裡「醫療保健夥伴」的角色，落地成一個具備情緒感知與陪伴能力的嵌入式 AI 實體。

---

## ✨ 專案簡介

AI Baymax Plushie 的核心理念，是將「絨毛娃娃」轉變為一個具備明確人設的語音 AI 角色，並透過邊緣運算與雲端 AI 的結合，實現以下能力：

- 低延遲語音喚醒（Wake Word）
- 語音轉文字（STT）
- 同理心式對話（LLM）
- 文字轉語音（TTS）
- 低溫加熱與溫暖觸感
- 呼吸燈與表情狀態反饋
- 頭部點頭、搖頭、揮手等安全動作

這個專案不只是單純的 AI 語音機器人，而是一個「擁有陪伴感與機械表現力」的嵌入式互動裝置。

---

## 🧠 核心功能

- 🎙️ 隨時喚醒（Wake Word）
  - 在邊緣端即時檢測喚醒詞
  - 可降低延遲與提升隱私保護

- 🧠 同理心大腦（Empathetic LLM）
  - 使用客製化 Prompt，讓 AI 以溫和、耐心、關懷的語氣回應
  - 特別適合心理陪伴與情緒安撫情境

- 🗣️ 自然語音對話（Voice I/O）
  - 整合 Whisper、OpenAI TTS、ElevenLabs 等語音工具
  - 提供接近自然的人類對話體驗

- 🔥 物理療癒感（Physical Warmth）
  - 加入低溫加熱墊，模擬擁抱時的暖意
  - 讓機器人不只「說話」而是「有溫度」

- 💡 呼吸狀態燈（Breathing LED）
  - 顯示待機、聆聽、思考、說話等狀態
  - 增加擬人化表現與互動感

- 🤝 安全的機械互動
  - 透過伺服機或有限動作實現點頭、搖頭、揮手
  - 所有動作都需有安全界限與受控範圍

---

## 🏗️ 系統架構圖

本專案採用「邊緣端 + 雲端 AI」的混合架構：

- 邊緣端（Raspberry Pi）負責喚醒、音訊處理、狀態燈與動作控制
- 雲端端（LLM / STT / TTS）負責語意理解與自然語音生成

這種方式兼顧了：

- 低延遲
- 保護隱私
- 高度自然的對話能力
- 物理互動與桌面 PoC 的可驗證性

```text
                          ┌──────────────────────────────┐
                          │          使用者 User         │
                          │  「哈囉杯麵」/「我今天不舒服」 │
                          └──────────────┬───────────────┘
                                         │
                                         ▼
                          ┌──────────────────────────────┐
                          │   絨毛娃娃內部（Edge）        │
                          │                              │
                          │  🎙️ 麥克風  →  🔍 喚醒詞引擎   │
                          │      ↓                       │
                          │  🍓 Raspberry Pi 4B / Zero 2W│
                          │      ↓                       │
                          │  🔊 音訊輸出  │  💡 狀態燈    │
                          │  🔥 低溫加熱墊 │ 🦾 伺服機    │
                          └──────────────┬───────────────┘
                                         │
                                         │  本地即時處理
                                         │
                          ┌──────────────▼───────────────┐
                          │      Edge AI / I/O Layer      │
                          │  - 音訊錄製                   │
                          │  - 喚醒詞判斷                 │
                          │  - 狀態控制                   │
                          │  - 動作觸發                   │
                          └──────────────┬───────────────┘
                                         │
                                         ▼
                          ┌──────────────────────────────┐
                          │      雲端 AI 服務（Cloud）    │
                          │                              │
                          │  👂 Whisper  →  🧠 LLM        │
                          │      ↓                       │
                          │  🗣️ TTS / OpenAI TTS         │
                          │                              │
                          │  角色：溫和、關懷、穩定的     │
                          │  AI 杯麵同理心大腦            │
                          └──────────────┬───────────────┘
                                         │
                                         ▼
                          ┌──────────────────────────────┐
                          │       AI 回應與互動輸出        │
                          │                              │
                          │  - 語音回應                  │
                          │  - 溫暖陪伴                  │
                          │  - 情緒與表情回饋            │
                          │  - 身心關懷對話              │
                          └──────────────────────────────┘
```

也可以用更簡潔的模組化版本：

```text
                   AI Baymax Plushie
 ┌──────────────────────────────────────────────────────────┐
 │                        User / Household                  │
 │            「哈囉杯麵」/「我有點不舒服」/「我想聊天」     │
 └──────────────────────────────┬─────────────────────────────┘
                                │
                                ▼
          ┌────────────────────────────────────────────────┐
          │       Plushie Hardware / Edge Layer          │
          │ Mic → Wake Word → Raspberry Pi → Speaker    │
          │ LED → Heater → Servo Motion → Safe control  │
          └───────────────────────┬────────────────────────┘
                                  │
                                  ▼
          ┌────────────────────────────────────────────────┐
          │        AI Processing / Cloud Layer           │
          │ STT → LLM → TTS → Empathetic Persona         │
          └────────────────────────────────────────────────┘
```

---

## 🧰 硬體需求

1. 機體外殼
   - 50cm–80cm 市售大白杯麵絨毛娃娃

2. 主控板
   - Raspberry Pi 4B（推薦）
   - Raspberry Pi Zero 2 W（若需更小型化）

3. 音訊模組
   - USB 麥克風
   - 迷你擴音喇叭 / 喇叭放大模組

4. 電力供應
   - 10000mAh 行動電源
   - 建議支援邊充邊放（pass-through charging）

5. 週邊耗材
   - 3D 列印防護殼
   - 散熱片 / 散熱模組
   - 拉鍊、魔鬼氈、固定材料

6. 可選擴充模組
   - 低溫加熱墊（約 38°C）
   - 狀態 LED
   - 伺服機（點頭 / 搖頭 / 揮手）

---

## 🛠️ 軟體技術棧

- 作業系統：Raspberry Pi OS / Linux
- 程式語言：Python 3
- 喚醒詞：Porcupine、Snowboy 或類似方案
- 語音辨識：Whisper API 或本地端 STT
- 語言模型：GPT-4o、Claude 或開源本地模型
- 文字轉語音：OpenAI TTS、ElevenLabs、或本地端 TTS
- 控制層：Python 背景服務 / Agent Logic

---

## 🚀 快速開始

### 1. 下載專案

```bash
git clone https://github.com/yourusername/AI-Baymax-Plushie.git
cd AI-Baymax-Plushie
```

### 2. 建立虛擬環境

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. 安裝依賴

```bash
pip install -r requirements.txt
```

### 4. 設定環境變數

建立 `.env` 檔案並填入 API 金鑰：

```env
OPENAI_API_KEY=your_openai_api_key
PICOVOICE_API_KEY=your_picovoice_api_key
```

### 5. 啟動桌面概念驗證（PoC）

先不要直接裝進娃娃內，先在桌面環境測試聲音輸入與輸出：

```bash
python main.py
```

---

## ⚠️ 安全警告

本專案涉及將電子元件裝進絨毛娃娃與棉花材質內部，存在明顯的火災、過熱與短路風險，因此安全設計必須被視為優先事項。

建議遵守以下原則：

- Raspberry Pi、電池與線路必須與棉花素材隔離
- 使用阻燃或耐熱的防護外殼
- 加入散熱孔與適當散熱設計
- 確保裸露板子不直接接觸布料或棉花
- 在測試過程中持續監控溫度
- 使用穩壓與正確電壓供電
- 專案仍屬原型階段，未經相關安全測試前請勿直接大量生產

---

## 📁 專案結構

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

## 📌 未來發展方向

未來可擴充的方向包括：

- 更強的本地喚醒詞與低延遲處理
- 更自然的中文 / 英文語音互動
- 更安全的伺服機控制與動作界限
- 更細緻的情緒模型與陪伴風格調校
- 更強的邊緣 AI 與本地模型整合
- 最終達成可持續使用的 AI 絨毛伴侶裝置

---

## 🤝 貢獻方式

歡迎任何形式的貢獻，包含但不限於：

- 改善語音流程
- 修正電路與安裝設計
- 優化 AI Prompt
- 製作可重複使用的 3D 結構
- 增加安全與測試文件

如果你有好點子或想協作實作，歡迎提交 Issue 或 Pull Request。

---

## 📜 授權說明

本專案僅供教育、研究與原型開發用途，請在實際改造任何消費性產品前，確認符合當地電子與安全法規要求。

---

## 🙏 致謝

本專案受益於 AI 絨毛玩具、邊緣運算、語音 AI 與智慧家電領域的相關創新思路。若能將這些技術整合成一個貼近人類陪伴感的互動裝置，便是一個具有實用價值與未來潛力的創作方向。

如果你想要，我也可以下一步幫你把這份 README 再整理成：
- 中英雙語版
- 更正式的 GitHub 官方專案頁面版
- 更精簡的短版 README
- 加上欄位 badges（stars / forks / license / build status）的版本
