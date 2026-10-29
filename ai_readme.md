# 🎈 AI Baymax Plushie (AI 杯麵絨毛機器人)

![](https://github.com/ting0813/AI-plush-giraffe/blob/main/Gemini_Generated_Image_xbjvv3xbjvv3xbjv.jpg?raw=true)

這是一個開源的軟硬體改造專案 (Modding Project)，旨在將市售的 50cm-80cm 「杯麵 (Baymax)」絨毛娃娃，改造成一台真實的、具備高度同理心與語音對話能力的 AI 伴侶機器人。

透過結合 Raspberry Pi、大型語言模型 (LLM) 以及語音辨識技術，我們將電影中的「個人醫療保健夥伴」帶入現實生活，為使用者提供身心靈的陪伴與療癒。

---

## ✨ 核心功能 (Features)

*   🎙️ **隨時喚醒 (Wake Word)**: 支援在地端運行的喚醒詞系統 (如 "Hello, Baymax")，低延遲且保護隱私。
*   🧠 **同理心大腦 (Empathetic LLM)**: 深度客製化的 Prompt，無論你說什麼，杯麵都會以溫和、不帶批判且關懷健康的態度回應。
*   🗣️ **自然語音對話 (Voice I/O)**: 整合 Whisper STT 與 OpenAI TTS (或 ElevenLabs)，達到接近真人的語音交談體驗。
*   🔥 **物理療癒 (Physical Warmth)**: 內建安全低溫加熱墊，擁抱時能感受到約 38°C 的仿生體溫。
*   🫀 **呼吸狀態燈 (Breathing LED)**: 內建 LED 模組，在 AI 思考或講話時發出柔和的呼吸光芒。

---

## 🏗️ 系統架構圖 (System Architecture)

本專案採用邊緣運算 (Edge) 與雲端 (Cloud) 混合架構。喚醒與基礎 I/O 由樹莓派處理，複雜的語意理解則交由雲端 API。

```mermaid
flowchart TD
    User((🧑 使用者))

    subgraph Edge[🧸 絨毛娃娃內部（Edge / Hardware）]
        Mic[🎙️ USB 麥克風]
        Wake[🔍 喚醒詞引擎\nPorcupine / Snowboy]
        RPi[🍓 Raspberry Pi 4B / Zero 2 W]
        Speaker[🔊 迷你擴音喇叭]
        LED[💡 呼吸式狀態燈]
        Heater[🔥 低溫加熱墊]
        Servo[🦾 伺服機 / 頭部動作]
    end

    subgraph Cloud[☁️ 雲端 AI 服務（Cloud）]
        STT[👂 語音轉文字\nWhisper API]
        LLM[🧠 同理心大腦\nGPT-4o / Claude]
        TTS[🗣️ 文字轉語音\nOpenAI TTS]
    end

    User -->|說話| Mic
    Mic --> Wake
    Wake -->|喚醒成功| RPi

    Mic -->|錄音檔| STT
    STT -->|文字內容| LLM
    LLM -->|回應文字| TTS
    TTS -->|音訊檔| RPi

    RPi --> Speaker
    Speaker -->|溫暖回應| User

    RPi -. 控制溫度 .-> Heater
    RPi -. 控制表情與燈光 .-> LED
    RPi -. 控制點頭 / 揮手 .-> Servo
```

這個架構讓喚醒與即時互動保留在邊緣端，讓杯麵具備快速反應與低延遲體驗；而語意理解與自然對話則透過雲端 AI 完成，形成「有溫度的硬體 + 有同理心的 AI」整合方案。

---

## 🛠️ 硬體清單 (Hardware Requirements)

1.  **軀殼**: 50cm 或 80cm 蝦皮市售大白杯麵絨毛娃娃。
2.  **主機**: Raspberry Pi 4B (推薦，算力較充足) 或 Raspberry Pi Zero 2 W (體積小)。
3.  **音訊**: 迷你 USB 收音麥克風 + 3.5mm 迷你擴音喇叭模組。
4.  **電源**: 10000mAh 支援邊充邊放的行動電源。
5.  **耗材**: 3D 列印保護殼 (防護電路板與棉花接觸)、拉鍊、魔鬼氈、散熱片。

---

## 🚀 快速開始 (Getting Started)

### 1. 軟體環境準備
```bash
# 複製專案
git clone https://github.com/yourusername/AI-Baymax-Plushie.git
cd AI-Baymax-Plushie

# 建立虛擬環境
python3 -m venv venv
source venv/bin/activate

# 安裝依賴套件
pip install -r requirements.txt
```

### 2. 環境變數設定
將 `.env.example` 重新命名為 `.env`，並填入你的 API Keys：
```env
OPENAI_API_KEY=your_openai_api_key
PICOVOICE_API_KEY=your_picovoice_api_key
```

### 3. 啟動對話測試 (桌面版 PoC)
先不要放入娃娃體內，在桌面上連接麥克風與喇叭進行測試：
```bash
python main.py
```

---

## ⚠️ 安全警告 (Safety Warning)

**防燃與散熱處理是本專案的重中之重！**
Raspberry Pi 運作時會產生高溫，請務必確保電路板與行動電源放置於**阻燃且具備散熱孔的 3D 列印塑膠盒**中，絕不可讓裸露的電路板直接接觸絨毛或棉花，以免引發火災危險。
