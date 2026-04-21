# Zrald CLI

```bash
npm install -g zraldcli
```

```bash
zralds
```

- Email: `freetrial@zraldwebdevelopmentservices.shop`
- License key: `ZRLD-AF7F-94C2-C7AC-B261-09DC-9E85`
- Policy: device cap `1,000,000` one-week expiry window starts when cap is reached



Mac Setup 


Install docker 
```bash
brew install --cask docker
```
Install Qdrant and Falkordb 
```bash
docker run -p 6333:6333 -p 6334:6334 \
    -v "$(pwd)/qdrant_storage:/qdrant/storage:z" \
    qdrant/qdrant
```
```bash
docker run -p 6379:6379 -p 3000:3000 \
    -it --rm falkordb/falkordb:latest
```


Best Combination for Cost-Effective Usage
(Ideal for ordinary tasks with low complexity.)

Main: Copilot GPT-5.4 Mini

Read: Copilot Gemini 3 Pro Preview

Write: Copilot GPT-5 Mini

Best Combination for Medium Complexity
(Balances high productivity with efficient token usage.)

Main: Claude 4.6 Sonnet

Read: Copilot Gemini 3 Pro Preview

Write: GPT-5.3 Codex

Best Combination for High Complexity
(Prioritizes optimal AI performance over token conservation.)

Main: Claude 4.7 Opus

Thinking: GPT-5.4 Pro Thinking

Read: Gemini 3.1

Write: Claude 4.7 Opus / GPT-5.4 Pro
<img width="637" height="174" alt="image" src="https://github.com/user-attachments/assets/88c4b687-9f01-4f2d-b7cf-d5197e08808e" />

## What Zrald CLI Does

Zrald CLI is a terminal-native AI coding agent focused on real engineering workflows:

- Complex bug fixing and refactoring
- Multi-step automation across real repositories
- Faster development with model routing, memory, and code intelligence

The product is the CLI workflow itself. Users can bring their own model/provider keys (BYOK).

## Key Capabilities

### 1) `/codeconfigure` model control

Zrald CLI supports `/codeconfigure` so users can tune how work is executed:

- Set a **Thinking Model** for planning/reasoning
- Set **Global Read** and **Global Write** models
- Configure **Global Fallback** read/write models
- Override model settings per tool when needed

This allows teams to keep a strong director model while assigning read/write-heavy operations to lower-cost models.

### 2) Token savings visibility (read + write)

Zrald highlights savings directly in usage output so users can see exactly where optimization happens:

- **Saved Token Usage Read**: tokens handled by configured read models
- **Saved Token Usage Write**: tokens handled by configured write models
- **Total Saved Token Usage**: combined offloaded token usage

This gives transparent cost insight for each session, especially on large coding tasks.

### 3) Self-Evolving workflow

Zrald includes a self-evolving execution review pattern designed to improve quality over time:

- Captures per-task execution notes in `Selfevolving/`
- Records best first moves, tool ratings, issues, and corrections
- Promotes durable lessons to persistent memory for future sessions

Result: better repeatability, fewer avoidable mistakes, and faster recovery when tasks fail.

### 4) Complex problem-solving with Code Index + Graph Index

Zrald uses both semantic and structural analysis to solve difficult coding problems safely:

- **Code Index**: semantic retrieval for intent-level discovery ("what does this part do?")
- **Graph Index**: dependency relationships and import/export paths ("what is connected to this file?")

Used together, they improve root-cause tracing, reduce duplicate work, and lower regression risk during edits.



- Website: https://zraldcli.zraldwebdevelopmentservices.shop

