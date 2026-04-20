# Allie — Taku's Workspace Partner

> A personal AI workspace built for Takunda Zanga. Context-aware thinking partner, editorial collaborator, skills lab, and daily pulse tracker — all in one file.

---

## What This Is

Allie is a single-file HTML app powered by the Anthropic Claude API. Four surfaces:

- **Home** — conversation with Allie across 5 modes (Think, Write, Challenge, Edit, Build) and 6 project contexts
- **Weekly** — pulse check: what's alive, what's draining, body, projects status
- **LBLS** — full poem tracker for *Lost But Loving Still* — click any poem to open an editorial session
- **Skills Lab** — contextual learning tied directly to what you're building

Allie knows who Taku is from the first word. No onboarding required.

---

## Project Structure

```
allie/
├── index.html     ← The entire app (HTML + CSS + JS in one file)
├── vercel.json    ← Vercel static deployment config
├── README.md      ← This file
└── CLAUDE.md      ← Instructions for Claude Code when editing locally
```

---

## Running Locally

Open `index.html` in a browser. That's it.

**Inside claude.ai** — API calls proxy automatically. No key needed.

**Outside claude.ai** (local browser or Vercel deploy) — you need your Anthropic API key. Find all three `fetch` calls in the `<script>` block and add to each one's headers:

```js
'x-api-key': 'sk-ant-api03-',
'anthropic-version': '2023-06-01',
'anthropic-dangerous-direct-browser-access': 'true'
```

> Never commit your API key to git.

---

## Deploying via GitHub + Vercel

Allie deploys automatically via the GitHub integration:

1. Push changes to the `main` branch of this repo
2. Vercel detects the push and redeploys automatically
3. Live in under 60 seconds

The `vercel.json` handles routing so Vercel knows `index.html` is the entry point.

---

## Iterating with Claude Code

For local edits, Claude Code is the right tool.

```bash
npm install -g @anthropic-ai/claude-code
cd /path/to/allie
claude
```

First thing to say: `"Read CLAUDE.md then tell me what you see"`

Example instructions:
- *"Make the sidebar narrower and increase feed font size"*
- *"Add a new skill card under NurSara: STT Provider Comparison"*
- *"Update the system prompt — NurSara just got its first user"*
- *"Add localStorage persistence for the main conversation thread"*

Iteration loop:
```
Edit in Claude Code → refresh browser → looks right → git push → live
```

---

## Architecture

### System prompt (`const ALLIE`)
The most important layer. Carries full context: all projects, Taku's communication style, mode-specific behaviour, ghost mentor framework, editorial methodology. Edit with care.

### Skills data (`const SKILLS`)
Array of skill cards. Each has: name, domain, type, description, projects, progress %, accent colour, opening prompt.

### Poem tracker
Static list of all LBLS poems by act and status. Click opens a modal with the full editorial methodology loaded — quiz first, excavate truth, ghost mentor, draft, lock.

### Today + Weekly persistence
Uses `localStorage` — saves daily check-in fields and weekly pulse so data survives page refreshes.

### Modal system
Both skill sessions and poem editorial sessions run in the same modal component with separate conversation histories so they don't bleed into each other.

---

## Planned Next

1. API key input field in the UI (so no code editing needed to deploy)
2. Persistent conversation memory across sessions (localStorage)
3. Skill progress persistence (update % after each session)
4. PIE dot generator mode
5. Voice input via Web Speech API

---

## The Bigger Picture

Allie is also a proof of concept for Sasce.

The core architecture — a deeply personalised system prompt that makes an AI feel like it genuinely knows you, without storing personal data on a server — is exactly what Sasce needs. Every design decision here (context over storage, voice over data, minimum necessary intelligence) is a Sasce design decision.

---

*Built by Takunda Zanga. Powered by Claude. Deployed on Vercel. Part of the A³I ecosystem.*

> "AGI competes for the horizon. A³I returns something to the person standing right here."
