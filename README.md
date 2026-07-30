# Craptcha-TTS: Real-Time Telegram Message Scraper & Voice Reader

[![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi&logoColor=00FFCC)](https://fastapi.tiangolo.com/)
[![Telethon](https://img.shields.io/badge/Telethon-37AEE2?style=for-the-badge&logo=telegram&logoColor=white)](https://github.com/LonamiWebs/Telethon)
[![Gemini Native Audio](https://img.shields.io/badge/Gemini%20Native%20Audio-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://github.com/google/generative-ai-python)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

> Telegram channel scraper and TTS reader built with Telethon, FastAPI, and Gemini Native Audio streaming for real-time 24kHz PCM voice playback.

Craptcha-TTS is a secure, hands-free text-to-speech scraper service. It enables users to authenticate their Telegram account via QR code or phone, browse synchronized channels, track unread reading pointers, and stream raw 24kHz PCM voice synthesized directly from Gemini's native audio streaming model.

---

## Interactive Trial Showcase

<div align="center">
  <a href="#" target="_blank">
    <img src="https://img.shields.io/badge/Interactive%20Trial-Local%20Setup%20Required-00C9A7?style=for-the-badge&logo=fastapi&logoColor=white" height="40" alt="TTS Local Trial" />
  </a>
</div>

### Running the Local Voice Reader:
1. Clone the repository and configure `.env` with your `TG_API_ID`, `TG_API_HASH`, `TG_TARGET_GROUP_ID`, and `GEMINI_API_KEY`.
2. Launch the FastAPI server:
   ```bash
   uvicorn main:app --reload --port 8000
   ```
3. Open `http://localhost:8000/docs` to interact with the API endpoints.
4. Initiate Telegram QR code authentication via `GET /auth/qr` or phone sign-in via `POST /auth/phone`.
5. Select a channel (`POST /channel/select`) and stream clean voice playback using `GET /voice/tts-stream?text=Hello`.

---

## Key Features

* **Multi-Stage Authentication**: Native Telethon authentication supporting long-polling QR login loops (`qr.png`), SMS verification codes, and Cloud 2FA passwords.
* **Low-Latency PCM Streaming**: Integrates `models/gemini-2.5-flash-native-audio-preview-12-2025` to yield binary 24kHz 16-bit mono PCM chunks directly into a FastAPI `StreamingResponse`.
* **Automated Text Cleaning**: Strips URLs and non-BMP supplementary emojis via regex to ensure seamless text-to-speech synthesis.
* **Stateful Channel Pointers**: Persists active channels and read message IDs to `state.json`, supporting forward and backward message traversal (`ahead`, `behind`, `current`).
* **Topic Forwarding Integrations**: Supports message forwarding directly into specified forum topics within Telegram groups (`ForwardMessagesRequest`).

---

## Architecture Overview

```
[ Telegram Channels ] ──► [ Telethon Scraper Engine ] ──► [ Text Sanitizer ]
                                                                 │
                                                    (Cleaned Message String)
                                                                 │
                                                                 ▼
[ User Web Browser ] ◄── (24kHz PCM Stream) ◄── [ Gemini Native Audio Live ]
```

---

## Repository Metadata & SEO Parameters

* **About Description**: Telegram channel scraper and TTS reader built with Telethon, FastAPI, and Gemini Native Audio streaming for real-time 24kHz PCM voice playback.
* **Target Topics**: `telegram-scraper`, `text-to-speech`, `telethon`, `gemini-audio`, `fastapi`, `python`, `pcm-streaming`, `tts-reader`.

---

## Environment Setup

Configure the `.env` file in the root directory:

```env
TG_API_ID=1234567
TG_API_HASH=your_telegram_api_hash
TG_TARGET_GROUP_ID=-100123456789
GEMINI_API_KEY=your_gemini_api_key
TG_DEVICE_MODEL=TTS-Reader-Local
TG_SYSTEM_VERSION=Windows 10
TG_APP_VERSION=1.0.0
```

---

## License

Distributed under the MIT License. See `LICENSE` for details.
