# Topics to Study — Pi-to-Pi Communication

## Goal
Understand how Pi-to-Pi communication works in practice so we can later design custom communication patterns for our own Pi workflows.

## Topics

### 1. System Goal
- What problem `coms.ts` solves
- Why session history is not enough
- Why peer-to-peer communication matters

### 2. Agent Identity
- `--name`
- `--purpose`
- session id
- how peers are distinguished

### 3. Discovery
- where agents register themselves
- how peers find each other
- registry structure and project scoping

### 4. Transport
- Unix sockets / named pipes
- how endpoints are created
- how a message moves between processes

### 5. Message Protocol
- message envelope structure
- `prompt`
- `response`
- `ping`
- `msg_id`
- timestamps
- hop count

### 6. Pi Integration
- how the extension plugs into Pi
- which extension hooks/events are involved
- how inbound messages become agent work

### 7. Tool Surface
- `coms_list`
- `coms_send`
- `coms_get`
- `coms_await`
- why this tool API works well for the model

### 8. Response Lifecycle
- pending messages
- waiting for replies
- completing the response flow
- correlation by message id

### 9. State and Lifecycle
- startup
- registration
- heartbeat / ping
- shutdown
- stale peer cleanup

### 10. Safety and Limits
- timeout behavior
- hop limits
- loop prevention
- audit/logging behavior

### 11. User Experience Layer
- peer widgets
- visible agent pool
- slash commands
- usability considerations

### 12. Designing a Custom Version
- which parts are essential
- what could be simplified
- alternatives to the current design

Possible alternatives:
- file-based communication
- RPC-based communication
- HTTP/SSE communication
- Obsidian-based task handoff
- shared note or queue models

### 13. Personal Use Cases
- note-taking companion agent
- Obsidian support agent
- research partner agent
- daily summary agent
- project memory agent

## Recommended Study Order
1. System goal
2. Agent identity
3. Discovery
4. Transport
5. Message protocol
6. Tool surface
7. Response lifecycle
8. Safety and limits
9. Custom design ideas

## Outcome We Want
By the end of this study, we should be able to:
- explain clearly why `coms.ts` works
- identify the core architectural pieces
- compare this approach with RPC/session-based thinking
- design a simpler or more specialized communication model for our own Pi setup
