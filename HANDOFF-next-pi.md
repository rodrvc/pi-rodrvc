# Handoff for the Next Pi Session

## Purpose
This workspace is being used to learn Pi deeply, especially around agent communication patterns and how they could support future personal workflows such as Obsidian-based work logging and support agents.

The next Pi session should help study, explain, and document how Pi-to-Pi communication works, and later help adapt those ideas to custom agents.

## Current Status
We successfully tested communication between two Pi instances using the `coms.ts` extension from the `pi-vs-claude-code` repository.

Main conclusion:
- Pi-to-Pi communication worked **without using session id as a live mailbox**.
- It worked through a custom Pi extension that provides discovery, transport, protocol, and tools.

## Key Links

### Official Pi documentation
- Main README:
  - `/home/rodvall/.nvm/versions/node/v24.13.1/lib/node_modules/@earendil-works/pi-coding-agent/README.md`
- RPC docs:
  - `/home/rodvall/.nvm/versions/node/v24.13.1/lib/node_modules/@earendil-works/pi-coding-agent/docs/rpc.md`
- SDK docs:
  - `/home/rodvall/.nvm/versions/node/v24.13.1/lib/node_modules/@earendil-works/pi-coding-agent/docs/sdk.md`
- Skills docs:
  - `/home/rodvall/.nvm/versions/node/v24.13.1/lib/node_modules/@earendil-works/pi-coding-agent/docs/skills.md`
- Extensions docs:
  - `/home/rodvall/.nvm/versions/node/v24.13.1/lib/node_modules/@earendil-works/pi-coding-agent/docs/extensions.md`

### Pi-to-Pi communication example repo
- Repo:
  - `https://github.com/disler/pi-vs-claude-code`
- Relevant files:
  - `extensions/coms.ts`
  - `extensions/coms-net.ts`
  - `README.md` section: Pi-to-Pi Agent-to-Agent Communication

## Local Working Repo / Notes
- Local planning repo:
  - `/home/rodvall/pi-rodrvc`
- Public GitHub repo:
  - `https://github.com/rodrvc/pi-rodrvc`

Important files in this repo:
- `ROADMAP.md`
- `NOTES-pi-to-pi-coms.md`
- `TOPICS-coms-study.md`

## Key Deductions Already Made

### 1. Session is not the same as live communication
A Pi session stores history and metadata.
It can resume context, but by itself it is not a live channel into another running interactive Pi process.

### 2. Pi-to-Pi communication can be added through extensions
The working example uses a custom extension instead of relying on `--session`.

### 3. The architecture can be understood as 5 core parts
- discovery
- transport
- protocol
- agent integration
- tool surface

### 4. `coms.ts` uses local peer-to-peer communication
It appears to use:
- registry files for discovery
- Unix sockets / named pipes for transport
- tool-based interaction for the model

### 5. This is promising for future custom workflows
Possible future uses:
- note-taking helper agent
- Obsidian support agent
- work summary agent
- specialized peer agents for different tasks

## What the Next Pi Should Do

### First
Read these files completely:
- `/home/rodvall/pi-rodrvc/NOTES-pi-to-pi-coms.md`
- `/home/rodvall/pi-rodrvc/TOPICS-coms-study.md`
- `/home/rodvall/.nvm/versions/node/v24.13.1/lib/node_modules/@earendil-works/pi-coding-agent/docs/extensions.md`
- `/home/rodvall/.nvm/versions/node/v24.13.1/lib/node_modules/@earendil-works/pi-coding-agent/docs/rpc.md`
- relevant sections of `https://github.com/disler/pi-vs-claude-code`

### Then
Help study `coms.ts` in a structured order:
1. identity and CLI flags
2. registry/discovery
3. local transport
4. envelope/message protocol
5. tool registration
6. response lifecycle
7. cleanup, heartbeat, and safety rules

### Output Style Wanted
The user prefers:
- concise explanations
- practical reasoning
- clear distinctions
- structure over noise
- short but precise answers

### Most Helpful Behavior
The next Pi should:
- explain why each part exists
- connect the extension design to Pi architecture
- compare this approach with RPC and session-based thinking
- help translate the pattern into custom designs for personal workflows

## Immediate Next Task Suggestion
Start by breaking down `extensions/coms.ts` into sections and documenting:
- what each section does
- why it exists
- what assumptions it makes
- how we could replace it with a custom implementation later

## Notes About Repository Safety
The `pi-rodrvc` GitHub repo was reviewed before making it public.
Current public content is only planning and learning notes; no secrets were intentionally uploaded.
