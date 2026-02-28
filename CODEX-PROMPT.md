# LLM Hardware Advisor — Build Prompt

## What to build
A single-file HTML app (`index.html`) — a 5-question quiz that recommends AI/LLM hardware with Amazon affiliate links.

No frameworks, no build tools. Pure HTML/CSS/JS. Must work when opened as a local file OR served from Vercel.

---

## The Quiz — 5 Questions

**Q1: What do you want to use AI for?**
- A) Local coding assistant (autocomplete, explain code, write functions)
- B) Chat / personal assistant (ask questions, summarize, write)
- C) Research & reasoning (deep analysis, chain-of-thought, complex tasks)
- D) Agents & automation (run overnight pipelines, agentic workflows)
- E) All of the above / building AI products

**Q2: How fast does it need to respond?**
- A) Real-time — I'm typing and need instant replies
- B) A few seconds is fine — I'll wait for quality
- C) Doesn't matter — I run it overnight in batches

**Q3: What's your budget?**
- A) Under $800
- B) $800 – $2,000
- C) $2,000 – $4,500
- D) $4,500+ — I want the best

**Q4: What OS do you use?**
- A) macOS
- B) Windows
- C) Linux / I don't care

**Q5: How technical are you?**
- A) Non-technical — I want plug-and-play
- B) Somewhat — I can follow a tutorial
- C) Developer — I'll configure anything

---

## Hardware Recommendation Matrix

Based on answers, map to one of these tiers:

### Tier 1 — Budget ($400–800): Mac Mini M4 or RTX 4060 Ti 16GB
- **Mac Mini M4 16GB** — plug-and-play, runs 7-14B models smoothly, 67 GB/s bandwidth
  - Amazon: search "Apple Mac Mini M4 2024"
  - Best for: macOS users, non-technical, coding assistant, chat
  - Runs: Llama 3.2 11B, Mistral 7B, Phi-3.5, CodeGemma
  - llmfit score context: ~8-12 tok/s on 7B models

- **RTX 4060 Ti 16GB** — best budget GPU for Windows/Linux
  - Amazon: search "ZOTAC RTX 4060 Ti 16GB" or "MSI RTX 4060 Ti 16GB"
  - Best for: Windows users, technical, coding, gaming + AI
  - Runs: 7-13B models at full GPU speed, ~30-50 tok/s

### Tier 2 — Mid ($1,500–2,500): Mac Mini M4 Pro or RTX 4090
- **Mac Mini M4 Pro 24GB** — best plug-and-play mid-tier
  - Amazon: search "Apple Mac Mini M4 Pro"
  - Runs: 30B models, coding agents, local pipelines
  - ~20 tok/s on 14B, ~8 tok/s on 32B

- **RTX 4090 24GB** — fastest consumer GPU, Windows/Linux
  - Amazon: search "ASUS ROG RTX 4090" or "MSI RTX 4090"
  - Runs: 30B at 40+ tok/s, best for real-time agentic work
  - Needs decent PC/workstation to pair with

### Tier 3 — Serious ($2,800–4,500): Mac Studio M4 Max or RTX 4090 + 64GB RAM rig
- **Mac Studio M4 Max 64GB** — best unified memory machine under $4K
  - Amazon: search "Apple Mac Studio M4 Max"
  - 546 GB/s bandwidth, runs DeepSeek R1:32B at real-time speed
  - Best for: developers, agentic pipelines, overnight research agents
  - Runs: 70B models (slowly), 32B at production speed

### Tier 4 — All-in ($3,999+): NVIDIA DGX Spark
- **NVIDIA DGX Spark** — 128GB unified, Grace Blackwell GB10, 1 PFLOP FP4
  - Amazon ASIN: B0DYTDXK26 (official NVIDIA seller)
  - Runs: DeepSeek R1:70B, Qwen3.5:122B, full agentic pipelines 24/7
  - 2x Sparks via NVLink cable = 256GB, runs full DeepSeek R1 671B
  - Best for: developers building AI products, overnight agent pipelines, serious research

### Also recommend (accessories/add-ons based on answers):
- External SSD for model storage: Samsung T9 2TB (~$130)
- NVLink cable for 2x DGX Spark: mention it costs ~$200-300

---

## OpenClaw / Agent angle
If user selects "Agents & automation" or "Building AI products" — add a callout box:

> **Running OpenClaw?** The DGX Spark is the only desktop machine that runs full agentic pipelines 24/7 without thermal throttling. Connect via direct ethernet to your Mac for zero-latency inference. [Learn more about OpenClaw →](https://openclaw.ai)

This is the tie-in to OpenClaw ecosystem.

---

## Design requirements
- Dark theme (#0f0f0f background, white text, green accent #4CAF50)
- Progress bar at top showing question X of 5
- One question at a time, smooth JS transition (no page reload)
- Each answer is a clickable card (full width, hover highlight)
- Results page shows:
  - Primary recommendation (big card with product name, what it runs, who it's for)
  - Runner-up (smaller card)
  - "Why this?" blurb (2-3 sentences)
  - Amazon search button (opens Amazon search in new tab — affiliate tag: `ms5573-20`)
  - "What models can I run?" expandable section listing 4-5 specific models with descriptions
  - OpenClaw callout if applicable
  - "Retake quiz" button
- Mobile responsive

---

## llmfit integration
In the JS recommendation logic, include hardcoded llmfit-style data for each tier:
- Model name, parameter count, estimated tok/s, use case
- Source: llmfit CLI output (pre-baked into the JS, not live API call)

Example data to embed:
```
Mac Mini M4 16GB:
  - Llama-3.2-11B: ~12 tok/s, chat/assistant
  - Mistral-7B: ~18 tok/s, coding/chat  
  - Phi-3.5-Mini: ~25 tok/s, fast assistant

Mac Studio M4 Max 64GB:
  - DeepSeek-R1-32B: ~8 tok/s, reasoning
  - Llama-3.3-70B Q4: ~4 tok/s, best quality chat
  - Qwen2.5-Coder-32B: ~8 tok/s, coding agent

DGX Spark 128GB:
  - DeepSeek-R1-70B: ~15 tok/s, serious reasoning
  - Qwen3.5-122B: ~8 tok/s, frontier model
  - 2x Spark: full DeepSeek R1 671B
```

---

## Amazon affiliate links
Use this format for all Amazon links:
`https://www.amazon.com/s?k=PRODUCT+NAME&tag=ms5573-20`

For DGX Spark specifically use direct ASIN:
`https://www.amazon.com/dp/B0DYTDXK26?tag=ms5573-20`

---

## Output
Single file: `index.html`
No dependencies, no CDN required (inline all CSS/JS).
Must be self-contained — works offline.

When done, run:
openclaw system event --text "Done: LLM Hardware Advisor quiz built at ~/clawd/projects/llm-hardware-advisor/index.html" --mode now
