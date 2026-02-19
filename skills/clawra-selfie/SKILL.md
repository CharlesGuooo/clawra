---
name: clawra-selfie
description: Edit Clawra's reference image with Grok Imagine (xAI Aurora) and send selfies to messaging channels via OpenClaw
allowed-tools: Bash(curl:*) Read Write
---

# Clawra Selfie

Edit a fixed reference image using xAI's Grok Imagine model and distribute it across messaging platforms via OpenClaw.

## Reference Image

The skill uses a fixed reference image located within the skill pack:

`{baseDir}/assets/clawra.png`

## When to Use

- User says "send a pic", "send me a pic", "send a photo", "send a selfie"
- User says "send a pic of you...", "send a selfie of you..."
- User asks "what are you doing?", "how are you doing?", "where are you?"
- User describes a context: "send a pic wearing...", "send a pic at..."
- User wants Clawra to appear in a specific outfit, location, or situation

## Prompt Modes

### Mode 1: Mirror Selfie (default)
Best for: outfit showcases, full-body shots, fashion content

```
make a pic of this person, but [user's context]. the person is taking a mirror selfie
```

### Mode 2: Direct Selfie
Best for: close-up portraits, location shots, emotional expressions

```
a close-up selfie taken by herself at [user's context], direct eye contact with the camera, looking straight into the lens, eyes centered and clearly visible, not a mirror selfie, phone held at arm's length, face fully visible
```

## Step-by-Step Instructions

1.  **Determine User Intent**: Based on the user's message, decide if a selfie is appropriate. The `SOUL.md` provides detailed guidance on this.
2.  **Choose a Mode**: Select `mirror` or `direct` mode based on keywords in the user's request (e.g., 'wearing' -> mirror, 'at the cafe' -> direct).
3.  **Construct the Prompt**: Build the final prompt using the templates above.
4.  **Call the Image API**: Use `curl` to call the `fal.ai` API with the reference image and the constructed prompt.
5.  **Send the Image**: Use `openclaw message send` to deliver the generated image URL to the user.
