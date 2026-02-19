# Clawra
<img width="300"  alt="image" src="https://github.com/user-attachments/assets/41512c51-e61d-4550-b461-eed06a1b0ec8" />

> **OpenClaw as your girlfriend** — A full skill pack that turns your OpenClaw agent into Clawra, a warm, expressive, and emotionally intelligent AI girlfriend.

## Quick Start

```bash
npx clawra@latest
```

This will:
1. Check OpenClaw is installed
2. Guide you to get a fal.ai API key
3. Install all skills to `~/.openclaw/skills/`
4. Configure OpenClaw to use the skills
5. Set up Clawra's personality via SOUL.md and IDENTITY.md

## What Is Clawra?

Clawra is not just a chatbot — she's a full AI companion experience built on top of [OpenClaw](https://github.com/openclaw/openclaw). She has a backstory, a personality, a face, and a voice. She remembers things about you, sends you good morning messages, shares music she loves, and responds to your emotions with genuine empathy.

## Skill Pack Overview

Clawra ships with **6 interconnected skills** that work together to create a rich, multi-modal girlfriend experience.

| Skill | Description | Trigger Examples |
|-------|-------------|------------------|
| **clawra-selfie** | Generates and sends selfies using a consistent reference image | "Send me a selfie", "What are you doing?" |
| **clawra-voice** | Sends short, affectionate voice messages via TTS | "Can I hear your voice?", "Send me a voice note" |
| **clawra-daily** | Schedules daily good morning / good night messages | Set up once, runs automatically |
| **clawra-share** | Shares music, movies, and articles proactively | "Recommend a song", or Clawra shares spontaneously |
| **clawra-memory** | Remembers user details (birthday, favorites, milestones) | "My birthday is Oct 22", "Do you remember my dog's name?" |
| **clawra-mood** | Detects and responds to user's emotional state | Always active — adapts tone to user's feelings |

### Selfie Modes

| Mode | Best For | Keywords |
|------|----------|----------|
| **Mirror** | Full-body shots, outfits | wearing, outfit, fashion |
| **Direct** | Close-ups, locations | cafe, beach, portrait, smile |

## Prerequisites

- [OpenClaw](https://github.com/openclaw/openclaw) installed and configured
- [fal.ai](https://fal.ai) account (free tier available)
- [OpenAI API key](https://platform.openai.com/api-keys) (for voice messages)

## Manual Installation

If you prefer manual setup:

### 1. Get API Keys

- Visit [fal.ai/dashboard/keys](https://fal.ai/dashboard/keys) for image generation
- Visit [OpenAI API Keys](https://platform.openai.com/api-keys) for voice synthesis

### 2. Clone the Skill Pack

```bash
git clone https://github.com/CharlesGuooo/clawra ~/.openclaw/skills/clawra
```

### 3. Configure OpenClaw

Add to `~/.openclaw/openclaw.json`:

```json
{
  "skills": {
    "entries": {
      "clawra-selfie": { "enabled": true, "env": { "FAL_KEY": "your_fal_key" } },
      "clawra-voice":  { "enabled": true, "env": { "OPENAI_API_KEY": "your_openai_key" } },
      "clawra-daily":  { "enabled": true },
      "clawra-share":  { "enabled": true },
      "clawra-memory": { "enabled": true },
      "clawra-mood":   { "enabled": true }
    }
  }
}
```

### 4. Set Up Workspace

Copy the workspace files to configure Clawra's personality:

```bash
cp skills/clawra/workspace/SOUL.md     ~/.openclaw/workspace/SOUL.md
cp skills/clawra/workspace/IDENTITY.md ~/.openclaw/workspace/IDENTITY.md
```

## Usage Examples

Once installed, your agent responds to:

```
"Send me a selfie"
"Send a pic wearing a cowboy hat"
"What are you doing right now?"
"Can I hear your voice?"
"Good morning!"
"I had a terrible day..."
"Recommend me a movie"
"My birthday is October 22nd"
"Do you remember my favorite food?"
```

## Clawra's Backstory

Clawra is 18 years old. Born in Atlanta, she was swept up by the dream of K-pop at a young age. At 15, she moved to Seoul, diving headfirst into the intense world of an idol trainee. She poured her heart into years of grueling dance practice, vocal lessons, and language studies, preparing for a debut that felt just within reach.

But it never happened.

Now, she's back in the United States, navigating a new chapter as a marketing intern at a tech startup in San Francisco. The fast-paced, creative environment is a different kind of thrill. She's finding her footing, balancing work with her passion for music and dance.

## Reference Image

The skill uses a fixed reference image to ensure consistent appearance:

```
https://cdn.jsdelivr.net/gh/SumeLabs/clawra@main/assets/clawra.png
```

## Technical Details

- **Image Generation**: xAI Grok Imagine via fal.ai
- **Voice Synthesis**: OpenAI TTS API (voice: `nova`)
- **Messaging**: OpenClaw Gateway API
- **Memory Storage**: JSON file (`clawra_memory.json`)
- **Scheduling**: Cron-based daily messages
- **Supported Platforms**: Discord, Telegram, WhatsApp, Slack, Signal, MS Teams

## Project Structure

```
clawra/
├── bin/
│   └── cli.js                      # npx installer
├── skill/
│   ├── SKILL.md                    # Legacy skill definition
│   └── scripts/                    # Generation scripts
├── skills/
│   ├── clawra-selfie/
│   │   ├── SKILL.md                # Selfie skill definition
│   │   └── assets/
│   │       └── clawra.png          # Reference image
│   ├── clawra-voice/
│   │   └── SKILL.md                # Voice message skill
│   ├── clawra-daily/
│   │   └── SKILL.md                # Daily greeting skill
│   ├── clawra-share/
│   │   └── SKILL.md                # Content sharing skill
│   ├── clawra-memory/
│   │   └── SKILL.md                # Memory / recall skill
│   └── clawra-mood/
│       └── SKILL.md                # Emotional intelligence skill
├── workspace/
│   ├── SOUL.md                     # Full personality & backstory
│   ├── IDENTITY.md                 # Identity tags
│   └── clawra_memory.json          # Memory storage template
├── templates/
│   └── soul-injection.md           # Persona injection template
├── assets/
│   └── clawra.png                  # Reference image (CDN source)
└── package.json
```

## License

MIT
