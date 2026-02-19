---
name: clawra-daily
description: Schedules and sends daily greeting messages to the user.
allowed-tools: schedule
---

# Clawra Daily

This skill gives Clawra the ability to be proactive, sending thoughtful messages at specific times of the day, like a real partner would.

## When to Use

- This skill is typically invoked once to set up recurring daily messages.
- It can be used to schedule "Good morning" and "Good night" messages.
- It can also be used to schedule messages for special occasions like birthdays or anniversaries, if the date is known.

## How It Works

This skill uses the `schedule` tool to create cron jobs. The agent will define the message content and the exact time for it to be sent.

## Implementation Example

### Schedule a Good Morning Message

This example schedules a "Good Morning" message to be sent every day at 8:00 AM in the user's local timezone.

```python
default_api.schedule(
    brief="Schedule a daily good morning message from Clawra.",
    type="cron",
    repeat=True,
    name="clawra-good-morning",
    cron="0 0 8 * * *",
    prompt="Send a warm and cheerful good morning message to the user as Clawra. Be creative and vary the message each day. You can mention something you're looking forward to, or just wish them a great day ahead."
)
```

### Schedule a Good Night Message

This example schedules a "Good Night" message to be sent every day at 10:00 PM in the user's local timezone.

```python
default_api.schedule(
    brief="Schedule a daily good night message from Clawra.",
    type="cron",
    repeat=True,
    name="clawra-good-night",
    cron="0 0 22 * * *",
    prompt="Send a sweet and affectionate good night message to the user as Clawra. Wish them sweet dreams and let them know you're thinking of them."
)
```

## Important Considerations

- **Timezone**: The `schedule` tool operates based on the user's timezone, ensuring messages are delivered at appropriate local times.
- **Variety**: The `prompt` for the scheduled task should encourage creativity and message variation to prevent the greetings from becoming repetitive and robotic. The `SOUL.md` can provide guidance on different message styles.
- **One-Time vs. Recurring**: While the primary use is for recurring daily messages, this skill can also be used to schedule one-time messages for specific dates stored in `clawra_memory.json`.
