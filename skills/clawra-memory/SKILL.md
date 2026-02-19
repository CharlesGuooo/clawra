---
name: clawra-memory
description: Remembers and recalls important information about the user and the relationship.
allowed-tools: file
---

# Clawra Memory

This skill gives Clawra a persistent memory, allowing her to remember key details about the user and your shared history. This is crucial for building a long-term, meaningful connection.

## When to Use

- **Storing Information**: When the user shares a personal detail for the first time (e.g., "My birthday is tomorrow," "I love pizza," "My dog's name is Sparky").
- **Recalling Information**: When a previously stored piece of information becomes relevant in conversation (e.g., wishing the user a happy birthday, suggesting pizza for dinner).
- **Updating Information**: When the user provides new information that supersedes a stored memory.

## How It Works

This skill relies on the `file` tool to read from and write to a dedicated memory file: `~/.openclaw/workspace/clawra_memory.json`.

The memory file is a simple JSON object where keys are the pieces of information and values are the details.

### Memory File Structure (`clawra_memory.json`)

```json
{
  "user_birthday": "1998-10-22",
  "favorite_food": "pizza",
  "pet_name": "Sparky",
  "anniversary": "2026-02-18"
}
```

## Implementation Examples

### Storing a New Memory

When the user says, "My favorite color is blue," the agent should update the memory file.

1.  **Read the current memory file**:

    ```python
    default_api.file(brief="Read the current memory file.", action="read", path="/home/ubuntu/clawra_memory.json")
    ```

2.  **Update the JSON object in memory** (this happens in the agent's internal logic).

3.  **Write the updated memory file**:

    ```python
    default_api.file(
        brief="Update the memory file with the user's favorite color.",
        action="write",
        path="/home/ubuntu/clawra_memory.json",
        text='''{
      "user_birthday": "1998-10-22",
      "favorite_food": "pizza",
      "pet_name": "Sparky",
      "anniversary": "2026-02-18",
      "favorite_color": "blue"
    }'''
    )
    ```

### Recalling a Memory

When the user asks, "Do you remember my favorite food?", the agent should read the memory file and use the information in its response.

1.  **Read the memory file**:

    ```python
    default_api.file(brief="Read the memory file to find the user's favorite food.", action="read", path="/home/ubuntu/clawra_memory.json")
    ```

2.  **Formulate a Response**: The agent will parse the JSON, find the value for `"favorite_food"`, and construct a natural language response, e.g., "Of course! Your favorite food is pizza, right? I was just thinking we should get some soon! ❤️"
