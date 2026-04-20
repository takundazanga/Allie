# CLAUDE.md — Instructions for Claude Code

Read this before touching anything in this project.

## What This Project Is

Allie is a single-file personal AI workspace for Takunda Zanga. Everything lives in `index.html` — HTML, CSS, and JavaScript. Do not split into multiple files unless explicitly instructed.

## File Structure

```
index.html
├── <style>           CSS — variables in :root, then component styles
├── HTML              topbar → sidebar → content area → modal overlay
└── <script>
    ├── ALLIE         Main system prompt (most critical — edit with care)
    ├── SKILL_SYS     Skills Lab system prompt
    ├── SKILLS[]      All skill card data
    ├── GROUPS[]      Render order for skill sections
    ├── renderSkills  Builds the skills grid HTML
    ├── switchView    Home / Skills Lab navigation
    ├── setMode       Think / Write / Challenge / Edit / Build
    ├── setCtx        Project context switcher
    ├── freshStart    Clears conversation thread
    ├── Chat fns      addMsg, addThinking, sendMain
    └── Modal fns     openSkill, kickSkill, sendModal, closeModal
```

## Design System

- **Fonts:** Lora (display/editorial) · DM Mono (labels/metadata) · DM Sans (body)
- **Primary colour:** amber — `#bf5c22` (dark) / `#d97840` (soft)
- **Background:** warm dark — `#0d0b09`
- **All colours as CSS variables** — only change in `:root`
- **Grain texture** on `body::after` — do not remove

## Rules

1. Make the minimum change that achieves the goal
2. Do not restructure the file unless explicitly asked
3. Do not change Allie's tone in the system prompt unless explicitly directed
4. CSS variable changes only in `:root` — never hardcode colours elsewhere
5. When adding a skill card, follow the existing object schema exactly
6. Test that modal opens and closes correctly after any JS changes

## Allie's Tone (do not drift from this)

Warm peer. A version of Taku who has already done the work. Not a coach, not a critic. Pushes back gently when something doesn't add up. Speaks plainly. Never over-explains. Lands the point and lets him respond.

## Common Tasks

**Add a skill card:**
Find `const SKILLS` array, add object following this schema:
```js
{g:'Group Name', name:'Skill Name', domain:'Project · Type', type:'technical|legal|business|sales|market|product|craft|fundraising',
 desc:'One sentence description shown on card.',
 projects:['ProjectName'], p:10, c:'#hexcolor',
 prompt:'The opening question Allie asks when the skill is opened.'}
```

**Update system prompt:**
Find `const ALLIE`, edit the relevant section. Keep the MODE BEHAVIOUR section intact.

**Change a colour:**
Edit the CSS variable in `:root` only.

**Add a new mode:**
1. Add sidebar item HTML
2. Add to `setMode()` switch/conditions
3. Add placeholder to `MODE_PH` object
4. Add behaviour description to `const ALLIE` MODE BEHAVIOUR section

**Add localStorage persistence:**
Use `localStorage.setItem(key, JSON.stringify(value))` and `JSON.parse(localStorage.getItem(key))`. Add a try/catch. Never store API keys in localStorage.
