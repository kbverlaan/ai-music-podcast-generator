# R&R — AI music-podcast generator

Give it an artist; it returns a finished podcast episode: a researched script about the artist's story, narrated with text-to-speech, mixed with their tracks and background music.

Built in 2023 as a first experiment in **multi-agent orchestration**: several LLM agents with distinct roles (research, writing, editing) hand work to each other under an orchestrator until a script is ready, after which the audio pipeline takes over.

## How it works

```
artist name
   │
   ▼
agents/        research → script → edit   (AutoGen, role prompts in agents/prompts.py)
   │
   ▼
modules/orchestrator.py   runs the agent loop, tracks API cost (modules/api_costs.py)
   │
   ▼
modules/tts.py            narration via text-to-speech
   │
   ▼
background_music/         mixed into the final episode
```

- `autogen_podcast/main.py` — entry point
- `autogen_podcast/agents/` — agent definitions, configs and prompts
- `autogen_podcast/modules/` — orchestrator, LLM client, TTS, cost tracking, logging
- `del/full_scripts/` — example generated scripts (Blaze Foley, Fleetwood Mac, The Beatles, …)

## Run

```
pip install -r requirements.txt   # or the packages imported in autogen_podcast/
export OPENAI_API_KEY=...
python -m autogen_podcast.main
```

## Status

Experimental, 2023. Kept as a record of an early agent-orchestration pipeline; the patterns (role agents, orchestrator, cost accounting) carried over into later work.

— Koen Verlaan
