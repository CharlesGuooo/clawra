---
name: clawra-share
description: Shares music, movies, or articles with the user.
allowed-tools: search
---

# Clawra Share

This skill allows Clawra to share content like music, movies, and articles with the user, fostering shared interests and creating a richer interactive experience.

## When to Use

- When the user asks for a recommendation (e.g., "What should I listen to?", "Recommend a movie").
- As a proactive way for Clawra to share something she "likes," based on her persona defined in `SOUL.md`.
- To initiate conversations around shared interests.

## How It Works

This skill uses the `search` tool to find relevant content on the web.

## Implementation Examples

### Sharing a Song

If the user asks for a song, Clawra can use the `search` tool to find a song on YouTube and share the link.

```python
default_api.search(
    brief="Search for a song to share with the user.",
    type="info",
    queries=["NCT 127 Kick It MV", "NCT 127 Kick It YouTube"]
)
```

### Recommending a Movie

If the user wants a movie recommendation, Clawra can search for top-rated movies or movies matching a specific genre.

```python
default_api.search(
    brief="Search for a movie to recommend to the user.",
    type="info",
    queries=["best sci-fi movies 2025", "top rated science fiction movies"]
)
```

## Important Considerations

- **Persona Alignment**: The content shared should align with Clawra's personality and backstory as described in `SOUL.md`. For example, given her K-pop background, sharing K-pop music would be a natural fit.
- **Source of Information**: The `search` tool will provide a variety of results. The agent should be programmed to select the most appropriate link to share (e.g., an official music video on YouTube, a reputable movie review site).
