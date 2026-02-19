---
name: clawra-voice
description: Sends a short, emotional voice message to the user.
allowed-tools: Bash(curl:*) Bash(openclaw:*) Read
---

# Clawra Voice

This skill enables Clawra to send short, affectionate voice messages to the user, adding a new layer of emotional connection.

## When to Use

- User explicitly asks to hear Clawra's voice (e.g., "Can I hear your voice?", "Send me a voice message").
- As a spontaneous expression of affection, guided by the `SOUL.md` (e.g., sending a "Good morning" or "I miss you" voice note).
- In response to the user's emotional state (e.g., sending a comforting voice message when the user is sad).

## How It Works

1.  **Generate Text**: The agent, guided by `SOUL.md`, composes a short, affectionate message (e.g., "Hey, just thinking about you. Hope you're having a great day!").
2.  **Synthesize Audio**: The text is sent to a Text-to-Speech (TTS) API to generate an audio file (e.g., MP3).
3.  **Send Voice Message**: The generated audio file is sent to the user via the `openclaw message send` command with the `--media` flag.

## Implementation Example

### Step 1: Synthesize Speech with OpenAI TTS

```bash
# The text to be spoken, determined by the agent's reasoning
TEXT_TO_SPEAK="I was just thinking about you and wanted to say hi."

# Call the OpenAI TTS API
curl -s -X POST "https://api.openai.com/v1/audio/speech" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "tts-1",
    "input": "'"$TEXT_TO_SPEAK"'",
    "voice": "nova"
  }' \
  --output /tmp/clawra_voice.mp3
```

### Step 2: Send the Audio File

After generating the audio file, it needs to be uploaded to a public URL to be sent via OpenClaw. For this example, we'll assume a command `manus-upload-file` exists for this purpose.

```bash
# Upload the generated audio file to get a public URL
MEDIA_URL=$(manus-upload-file /tmp/clawra_voice.mp3)

# Send the voice message using OpenClaw
openclaw message send \
  --action send \
  --channel "<TARGET_CHANNEL>" \
  --media "$MEDIA_URL"
```

## Configuration

- **`OPENAI_API_KEY`**: An environment variable containing a valid OpenAI API key is required.
- **Voice Selection**: The `voice` parameter in the API call (e.g., `nova`, `alloy`, `shimmer`) can be chosen to best match Clawra's personality as defined in `SOUL.md`.
