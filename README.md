# Zrald CLI

```bash
npm install -g zraldcli
```

```bash
zralds
```




To Use Code index (qdrant) and Graph Index (falkordb) you can set up locally using docker 

Mac Setup 


Install docker 



```bash
brew install --cask docker
```
After installing docker open it and configure necessary things before proceeding it is just a simple setup. 

Next lets create a directory for the qdrant and falkordb
```bash
mkdir -p "qdrant_storage"
```

```bash
mkdir -p "falkordb_data"
```
Install Qdrant and Falkordb 
```bash
docker run -d --name qdrant \
  -p 6333:6333 -p 6334:6334 \
  -v "$(pwd)/qdrant_storage:/qdrant/storage" \
  qdrant/qdrant
```
```bash
docker run -d --name falkordb \
  -p 6379:6379 \
  -v "$(pwd)/falkordb_data:/var/lib/falkordb/data" \
  falkordb/falkordb:latest
```


Windows Setup 


Install Docker 
https://www.docker.com/products/docker-desktop

Install Qdrant and Falkordb 
PowerShell
```bash
mkdir qdrant_storage -Force
mkdir falkordb_data -Force
```
```bash
docker run -d --name qdrant `
  -p 6333:6333 -p 6334:6334 `
  -v "${PWD}\qdrant_storage:/qdrant/storage" `
  qdrant/qdrant
```
```bash
docker run -d --name falkordb `
  -p 6379:6379 `
  -v "${PWD}\falkordb_data:/var/lib/falkordb/data" `
  falkordb/falkordb:latest
```



Linux Setup (Qdrant + FalkorDB)

   (Ubuntu/Debian)
```bash
sudo bash -c 'apt-get update && apt-get install -y docker.io curl && systemctl enable --now docker && mkdir -p qdrant_storage falkordb_data && docker rm -f qdrant falkordb >/dev/null 2>&1 || true && docker run -d --name qdrant -p 6333:6333 -p 6334:6334 -v "$PWD/qdrant_storage:/qdrant/storage" qdrant/qdrant && docker run -d --name falkordb -p 6379:6379 -v "$PWD/falkordb_data:/var/lib/falkordb/data" falkordb/falkordb:latest && sleep 4 && curl -fsS http://localhost:6333/ && echo && docker exec falkordb redis-cli PING'
```




Open Zrald cli make sure you install it using the npm install -g zraldcli

In terminal type:   zralds 

<img width="764" height="559" alt="image" src="https://github.com/user-attachments/assets/3e92daf7-edaa-4149-b312-ac85b0868f75" />

You can connect to a provider using the command /connect 

<img width="1907" height="1072" alt="image" src="https://github.com/user-attachments/assets/12fb9f67-44da-4634-9aad-9b1fd9ef6406" />

AI coding agents often hallucinate in large codebases not because they are “bad,” but because no model can reliably hold and reason over every file at once, so retrieval quality becomes the real bottleneck; that is why combining /codeindex (Qdrant) and /graphindex (FalkorDB) is effective: Qdrant provides fast semantic search to surface the most relevant code by meaning, while FalkorDB adds structural awareness of imports and dependencies so the agent can see what is connected before making changes, and together they answer both “what should I edit?” and “what else could this impact?”, which significantly reduces missed files, fragile edits, and hallucinated assumptions.


Use /codeindex to set up Qdrant.
Use /graphindex to configure your graph index.

You will need an AI model for embeddings.
For simple coding tasks, you can use OpenAI or run Ollama locally.
For complex coding, I suggest using Voyage Code 3.

<img width="541" height="284" alt="image" src="https://github.com/user-attachments/assets/537b5b74-43f7-4725-b2b0-688d1d37705f" />

"You only need to set up the embedding model for the Code Index.
Next is the highly useful /codeconfigure tool, which allows you to assign various AI models to specific tasks. This feature allows you to save tokens by offloading operations like file reading, file writing, and complex reasoning from your primary AI agent to other models.
Please maximize your terminal window to ensure both the left and right side panels of the Zrald CLI are fully visible.
Click /codeconfigure in the top right corner to reveal these options:"


<img width="465" height="610" alt="image" src="https://github.com/user-attachments/assets/330bccf1-d721-46ae-a84f-e610851ff825" />

"Here, you can easily configure the Thinking model. To save tokens, it is recommended to use this only for complex tasks. This section displays your connected accounts, so please ensure they are properly linked.
In the Global settings, you can assign a model for all Read and Write operations. We recommend scrolling down to view other tools, such as Memory Write and Read, where you can assign a less expensive AI model.
The Global Fallback acts as a backup if the primary Global model fails, such as when your subscription credits are depleted."




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

But you can do your own experiment.


Here you can see the Token Save Usage 

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

