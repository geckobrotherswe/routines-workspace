# routines-workspace

Stub workspace repo for Claude Code remote routines (https://claude.ai/code/routines).

## Why this exists

Remote routines clone a git source at run start. The agent inside the routine often doesn't actually need that repo — it might just be doing web searches, hitting an API, or composing and posting to a webhook. But the runner still wants *something* to clone.

This repo serves as that "something." It's intentionally empty. Routines clone it, ignore its contents, do their work in `/tmp` or the cwd, and post their output elsewhere (Mattermost webhook, email, etc.).

## Design notes

- **Public on purpose.** The routine runner clones unauthenticated, so private repos 404. If you tried to use a private repo here you'd get a generic "Failed to start run" with no useful error.
- **Don't put anything sensitive here.** It's public. Treat it like a town square noticeboard — nothing here is private.
- **Don't put anything important here either.** Routines may write to the cwd while running. Always do work in `/tmp` or the agent's scratch dir, not in this repo. Don't commit from inside a routine.

## Routines that use this

- `SAAB weekly read` (`trig_01PRbnGmb5A6FitN95hf1FuZ`) — Mondays 06:00 UTC, posts to Mattermost #saab via incoming webhook

(Add new ones here as you create them, so future-you knows what's pointing at this repo.)
