# Nyaya: The Voice of Justice

Nyaya is an AI-powered Indian legal voice assistant that integrates Twilio and Deepgram via websockets for real-time audio streaming and transcription. Nyaya delivers clear, accurate, and compassionate legal information through voice interactions, specializing in Indian law and common legal issues.

---

## Features

- **Real-time audio streaming:** Streams audio from Twilio, buffers, and forwards it to Deepgram for live transcription.
- **Voice-based user interaction:** Handles user barge-in and media streaming events, enabling natural voice conversations.
- **Customizable prompts:** Sends configuration and a legal assistant prompt to Deepgram on connection.
- **Response processing:** Processes Deepgram responses and relays them to Twilio.
- **Accessible explanations:** Explains legal rights, procedures, document requirements, and processes in simple, accessible language.

---

## Requirements

- Python 3.7+
- [`websockets`](https://pypi.org/project/websockets/) library
- [`python-dotenv`](https://pypi.org/project/python-dotenv/) for environment variable management

---

## Setup

1. **Install dependencies:**

    ```bash
    pip install websockets python-dotenv
    ```

2. **Set your Deepgram API key in a `.env` file:**

    ```env
    DEEPGRAM_API_KEY=your_deepgram_api_key_here
    ```

3. **Create a `config.json` file** with your Deepgram agent configuration.  
   Include a prompt that describes Nyaya's expertise, communication style, and the types of legal issues it can assist with.

---

## Usage

Start the server:

```bash
python your_script.py
```

The server listens on `localhost:5000` for incoming Twilio websocket connections.

## File Overview

- **sts_connect**: Establishes a websocket connection to Deepgram with authentication.
- **load_config**: Loads Deepgram agent configuration from `config.json`.
- **twilio_handler**: Manages the lifecycle of a Twilio connection and coordinates audio streaming between Twilio and Deepgram.
- **sts_sender/sts_receiver**: Send and receive audio and messages to/from Deepgram.
- **twilio_receiver**: Receives and buffers audio from Twilio, then forwards it to Deepgram.

## Notes

- Ensure your Twilio webhook is configured to connect to this server.
- The code includes placeholders for handling advanced features like function calling and order management.
- Nyaya is designed to help users navigate common legal problems such as consumer disputes, employment rights, property issues, government services, and legal documentation.

## Disclaimer

Nyaya provides information based on the knowledge of its underlying language model and should not be considered a substitute for professional legal advice. Its responses may not always be fully accurate or up-to-date. You can customize and extend this voice agent to better suit your specific requirements.
