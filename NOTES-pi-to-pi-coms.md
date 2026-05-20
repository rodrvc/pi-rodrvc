# Pi to Pi Communication Notes

## Context
This note records what we learned while testing communication between two Pi instances.

## What We Tested
We launched two separate Pi processes using the `coms.ts` extension from the `pi-vs-claude-code` repository.

Example launch style:

```bash
just local-coms --name alpha --purpose "Responder pong"
just local-coms --name beta --purpose "Enviar ping"
```

Then one instance sent a message to the other and received a response.

## Main Insight
This worked **without attaching to the other Pi by session id**.

Pi-to-Pi communication here is based on:
- a custom Pi extension
- peer discovery
- a local transport channel between running processes
- custom tools exposed to the model

## Important Distinction

### Session
A Pi session is mainly conversation history and metadata.

It helps Pi:
- resume context
- reopen saved work
- preserve history

A session is **not**, by itself, a live communication channel to another already-running interactive Pi process.

### Process Communication
To let one Pi talk to another live Pi, you need a communication mechanism.

In this case, that mechanism was provided by `coms.ts`.

## Why It Worked

### 1. The extension was loaded
Each Pi instance started with the `coms.ts` extension.

That extension adds:
- communication setup
- peer registry behavior
- extra tools
- custom flags such as `--name` and `--purpose`

### 2. Each Pi instance got an identity
Each process had a unique agent identity, such as:
- `alpha`
- `beta`

This made discovery and targeting possible.

### 3. Each Pi registered itself
The extension writes agent information to a shared registry under a path like:

```text
~/.pi/coms/projects/<project>/agents/<name>.json
```

That lets Pi peers discover each other.

### 4. Each Pi opened a local communication endpoint
On Linux/macOS, `coms.ts` uses Unix sockets.
On Windows, it uses named pipes.

So each running Pi becomes a reachable peer process.

### 5. The extension exposed communication tools
The model can use tools like:
- `coms_list`
- `coms_send`
- `coms_get`
- `coms_await`

This is the operational surface that enables Pi-to-Pi messaging.

## Internal Flow

### Startup
When `alpha` starts:
- it loads the extension
- opens a local endpoint
- writes its registry entry
- waits for messages

When `beta` starts:
- it does the same
- it can discover `alpha`

### Messaging
When `beta` sends a message:
- it uses a coms tool
- the extension sends a prompt envelope to `alpha`
- `alpha` processes the message
- `alpha` returns its assistant response
- `beta` waits for or polls the result

## Core Building Blocks
This pattern can be understood as 5 design pieces:

### 1. Discovery
How one agent finds another.

In this implementation:
- filesystem registry files

Possible alternatives:
- HTTP directory service
- Redis
- SQLite
- message broker
- Obsidian notes

### 2. Transport
How the message moves.

In this implementation:
- Unix sockets / named pipes

Possible alternatives:
- HTTP
- SSE
- WebSocket
- RPC
- file queues

### 3. Protocol
How messages are structured.

This repo uses envelope types like:
- `prompt`
- `response`
- `ping`

with metadata such as:
- `msg_id`
- sender info
- timestamps
- hop count

### 4. Agent Integration
How inbound messages are turned into something Pi can answer.

The extension bridges process-level messages into agent behavior.

### 5. Tool Surface
How the model uses the communication system.

This implementation exposes simple tools:
- list
- send
- get
- await

That makes the capability easy for the model to reason about.

## What We Learned
- Pi can talk to another Pi instance.
- This does not require sharing memory.
- This does not require using `--session` as a live mailbox.
- A custom extension can provide direct peer-to-peer communication.
- The clean design is: discovery + transport + protocol + tool surface.

## Why This Matters For Future Work
This opens the door to custom communication patterns for Pi, such as:
- note-taking companion agents
- specialized research peers
- production/dev agent pairs
- role-based Pi teams
- Obsidian-focused support agents

## Next Learning Step
Study `coms.ts` by sections:
1. identity and flags
2. registry and discovery
3. socket transport
4. message envelopes
5. tool registration
6. response lifecycle

## Change Log

### 2026-05-19
- Recorded first successful Pi-to-Pi communication learning notes
- Documented why the approach works
- Clarified session vs live communication
