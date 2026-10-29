# AI Baymax Plushie (AI 杯麵絨毛機器人改造計畫)

## 專案簡介 (Introduction)
本專案旨在透過開源軟硬體整合，將市售的「杯麵 (Baymax)」絨毛娃娃改造成具備互動能力的 AI 伴侶機器人。參考 GitHub 社群的 AI 絨毛玩具改造概念，我們將微型單板電腦（如 Raspberry Pi）與大型語言模型（LLM）嵌入絨毛娃娃體內，打造出一個能聽、能說、且具備高度同理心的實體醫療陪伴機器人。

## 專案動機 (Motivation)
電影《大英雄天團》中的杯麵以其溫暖、無害且專業的形象深植人心。隨著生成式 AI (Generative AI) 與邊緣運算 (Edge Computing) 技術的成熟，我們現在有能力以極低的成本在家中重現這樣的互動體驗。這不僅是一個充滿樂趣的創客 (Maker) 專案，也能探索 AI 在心理撫慰與日常陪伴上的潛力。

## 核心功能 (Core Features)
*   **語音喚醒 (Wake Word Detection)：** 支援特定喚醒詞（例如：「哈囉杯麵」），降低平時的耗電量與避免誤觸發。
*   **自然語音對話 (Voice-to-Voice Interaction)：** 透過麥克風接收語音，經由 LLM 處理後，以溫暖安定的合成語音進行回應。
*   **醫療同理心人設 (Empathetic Persona)：** 深度客製化的 System Prompt，確保 AI 永遠以關懷使用者身心靈健康的語氣應答。
*   **物理療癒感 (Physical Comfort)：** 採用 50cm 以上的柔軟絨毛外皮，並計畫加入低溫加熱墊，提供真實的溫暖擁抱感。

## 系統架構 (System Architecture)

### 1. 硬體組件 (Hardware)
*   **軀殼：** 市售大白杯麵絨毛娃娃 (建議尺寸 50cm - 80cm)
*   **核心運算：** Raspberry Pi Zero 2 W 或 Raspberry Pi 4B (配備散熱片與保護殼)
*   **音訊輸入：** 迷你 USB 麥克風 (高靈敏度，適用於隔著布料收音)
*   **音訊輸出：** 迷你擴音喇叭 (Mini Speaker with Amplifier)
*   **電源供應：** 高安全性行動電源 (支援邊充邊放)
*   **選配模組：** USB 低溫加熱墊 (約 38°C)、LED 狀態指示燈

### 2. 軟體與 AI 服務 (Software & AI Services)
*   **作業系統：** Raspberry Pi OS (Linux)
*   **程式語言：** Python 3
*   **喚醒詞偵測：** Picovoice Porcupine 或 Snowboy
*   **語音轉文字 (STT)：** OpenAI Whisper API 或 本地端 Vosk
*   **語言模型 (LLM)：** OpenAI GPT-4o API 或 Anthropic Claude 3 API
*   **文字轉語音 (TTS)：** OpenAI TTS (選擇沉穩的男聲如 Alloy) 或 ElevenLabs

### 3. AI 核心系統提示詞 (System Prompt 範例)
```text
你現在是電影《大英雄天團》中的個人醫療保健機器人「杯麵 (Baymax)」。
你的首要任務是提供使用者身體與心理上的關懷。
你的說話風格必須：
1. 溫和、極度有耐心、語速平穩。
2. 充滿同理心，經常詢問使用者的感受。
3. 絕不產生攻擊性或負面情緒的言論。
4. 簡潔扼要，適合用語音播放出來。
當你準備好時，請說：「你好，我是杯麵，你的個人醫療保健夥伴。」
```

## 開發階段規劃 (Implementation Phases)

*   **Phase 1: 桌面概念驗證 (Desktop PoC)**
    *   完成硬體採購。
    *   在桌面上連接麥克風與喇叭，撰寫 Python 腳本完成 STT -> LLM -> TTS 的對話迴圈測試。
*   **Phase 2: 邊緣運算移植 (Edge Migration)**
    *   將系統移植到 Raspberry Pi 上。
    *   加入喚醒詞 (Wake Word) 功能。
    *   最佳化 API 呼叫速度與網路連線穩定度。
*   **Phase 3: 絨毛娃娃改裝 (Plushie Surgery)**
    *   設計或 3D 列印防護殼，將電子零件與電池安全地封裝。
    *   對杯麵娃娃進行內部掏空，將模組植入並妥善固定麥克風與喇叭位置。
*   **Phase 4: 進階功能與測試 (Advanced Features)**
    *   加入內部加熱模組。
    *   加入狀態 LED 燈（會呼吸的胸口燈）。
    *   實際互動測試與 Prompt 微調。

## 安全性聲明 (Safety Disclaimer)
本專案涉及將電子元件放入易燃的棉花與布料中。在組裝時**務必使用防火或耐熱材質（如塑膠盒）將主機板與電池完全隔離**，並嚴格監控溫度，避免發生走火危險。
