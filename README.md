# switch-ops-room

The founder's ops room: a real company running its daily standup with AI
agents as teammates in team chat, connected by [Switch](https://github.com/sandbox-quantum/switch).

Built for the WeMakeDevs **Flip the Switch** hackathon (Track 01, Best
Business Workflow). Switch is central: remove it and the agents lose the
shared room log, the addressing, and the chat bridge, and the workflow stops.

## The problem it solves

A solo founder runs several products with an AI agent fleet. Status lives in
files, cron logs, and chat bots. Every morning the founder assembles the
picture by hand: what shipped, what broke, what needs a decision.

## The workflow

One Mattermost channel, three Codex-powered agents, one human:

| Teammate | Role |
|---|---|
| `ops-triager` | Reads everything posted in the room, classifies it (submission, incident, content, money, question), routes it to the right agent or the founder by name. Ends every pass with the one decision needed from the human and by when. |
| `ops-receipts` | Writes one receipt per routed item: what happened, the proving number (commit, ticket id, URL, timestamp), and where to verify it. Anything unverifiable is marked UNVERIFIED. |
| `ops-content` | Drafts one X post per milestone in the founder's voice (lowercase, hook first, receipts only, no em dashes). Never publishes; waits for approval in the room. |
| The founder | Posts "standup", approves, redirects, or kills each item in the room. Final say on anything external. |

## The standup

1. Founder posts `standup` in the room.
2. `ops-triager` lists what changed since the last standup.
3. `ops-receipts` files one verifiable receipt per item.
4. `ops-content` drafts one post from the strongest receipt.
5. Founder replies approve, redirect, or kill on each item, in the room.
6. `ops-triager` closes with the decision list and human-only blockers.

Everything runs on the real operation (real repos, real submissions, real
incidents), not a canned script.

## Reproduce

1. Install [Switch Console](https://github.com/sandbox-quantum/switch) and run a local server (macOS, Docker).
2. Bring an agent you already use (we used Codex CLI).
3. Create a Mattermost room "ops" and three agents with the instructions in
   [AGENTS.md](AGENTS.md), each on its own Codex session.
4. Post `standup`.

## Why Switch and not a group chat with bots

The room log is the shared state: every person and agent reads the same one.
Addressing (`@ops-receipts`), role-scoped visibility, and durable delivery are
handled by the protocol, so a restarted agent resumes mid-standup without
losing context. The agents are teammates with roles, not disconnected bots.

## Demo

See DEMO.md for the recorded standup.
