# Nyaya: The Voice of Justice

**An AI-powered Indian legal voice assistant that makes legal information accessible through natural, real-time voice conversations.**

Nyaya integrates **Twilio** and **Deepgram** via WebSockets to stream and transcribe audio instantly, responding with clear, accurate, and compassionate explanations specialized in Indian law and common legal issues.

---

## 🎯 What Nyaya Does

Nyaya listens to your voice, processes your legal questions, and responds in simple, accessible language to help you better understand your rights, legal procedures, and requirements. It's built with developers in mind, allowing customization of prompts and extension of capabilities for different legal use cases.

---

## ✨ Features

### For Users
- **🎤 Real-time legal conversations** — Ask questions naturally and get instant, spoken answers
- **📝 Accessible explanations** — Complex legal terms simplified into plain language  
- **🇮🇳 Indian law focus** — Configured to handle common queries about Indian legal topics
- **💬 Natural interactions** — Supports interruptions and barge-in for fluid conversations

### For Developers
- **🔄 Real-time audio streaming** — Streams audio from Twilio, buffers, and forwards to Deepgram for live transcription
- **⚙️ Customizable prompts** — Control Nyaya's expertise and tone through Deepgram prompt configuration
- **🎛️ Event handling** — Manages Twilio media streaming events and Deepgram transcription responses
- **🔧 Extensible architecture** — Built for customization and feature expansion

---

## 📋 Requirements

- **Python 3.7+**
- [`websockets`](https://pypi.org/project/websockets/) — WebSocket client library
- [`python-dotenv`](https://pypi.org/project/python-dotenv/) — Environment variable management
- **Twilio account** with WebSocket capabilities
- **Deepgram API key** with speech-to-speech features

---

## 🚀 Quick Setup

### 1. Install Dependencies
```bash
pip install websockets python-dotenv
```

### 2. Environment Configuration
Create a `.env` file in your project root:
```env
DEEPGRAM_API_KEY=your_deepgram_api_key_here
```

### 3. Agent Configuration
Create a `config.json` file with your Deepgram agent settings:
```json
{
  "type": "SettingsConfiguration",
  "audio": {
    "input": {
      "encoding": "mulaw",
      "sample_rate": 8000
    },
    "output": {
      "encoding": "mulaw",
      "sample_rate": 8000
    }
  },
  "agent": {
    "listen": {
      "model": "nova-2"
    },
    "think": {
      "provider": {
        "type": "open_ai_compatible",
        "model": "your-model-here"
      },
      "instructions": "You are Nyaya, an AI legal assistant specializing in Indian law..."
    },
    "speak": {
      "model": "aura-asteria-en"
    }
  }
}
```

### 4. Start the Server
```bash
python nyaya_server.py
```

The server will listen on `localhost:5000` for incoming Twilio WebSocket connections.

---

## 🏗️ Architecture Overview

### Core Components

- **`sts_connect`** — Establishes authenticated WebSocket connection to Deepgram
- **`load_config`** — Loads Deepgram agent configuration from `config.json`
- **`twilio_handler`** — Coordinates audio streaming lifecycle between Twilio and Deepgram
- **`sts_sender/sts_receiver`** — Bidirectional communication handlers for Deepgram
- **`twilio_receiver`** — Audio buffer management and forwarding to Deepgram

### Data Flow
1. **Twilio** captures user audio via phone call
2. **Audio streams** to Nyaya server via WebSocket
3. **Deepgram** processes speech-to-text transcription
4. **AI model** generates legal response
5. **Text-to-speech** converts response to audio
6. **Audio streams back** to user via Twilio

---

## 🔧 Configuration

### Twilio Setup
Configure your Twilio webhook to point to your Nyaya server:
```
wss://your-domain.com:5000/
```

### Customizing Legal Expertise
Edit the `instructions` field in `config.json` to customize:
- General legal focus
- Response tone and style
- Specific jurisdictions or topics
- Disclaimer requirements

---

## 📚 Example Topics Nyaya Can Handle

Nyaya can be configured to provide general information on:
- Consumer issues such as refunds and complaints
- Basic employment-related queries
- Property-related documentation and processes
- General information about government services
- Other common Indian legal topics supported by the configured prompt

---

## ⚠️ Important Notes

- **Development Status**: This project focuses on audio streaming and transcription.  
  Advanced features like function calling are placeholders for future development.
- **Webhook Configuration**: Ensure your Twilio webhook points to the correct server endpoint.
- **Performance**: Optimized for real-time conversations with minimal latency.
- **Extensibility**: Built for easy customization and feature additions.

---

## 🚨 Legal Disclaimer

**Nyaya provides general legal information based on its configuration and should never be considered a substitute for professional legal advice.**  

- Responses may not always be fully accurate or current with latest legal changes  
- Always verify important legal matters with qualified legal professionals  
- Use Nyaya as an educational tool and starting point for legal research  
- The developers assume no liability for decisions made based on Nyaya's responses  

---


