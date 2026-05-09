# Job Application Agent 🤖

An AI-powered autonomous agent that analyzes job postings against your resume, rewrites your resume bullets, identifies skill gaps, and generates a tailored cover letter — all in one click.

**[Live Demo →](https://YOUR-USERNAME.github.io/job-application-agent)**

---

## What it does

Paste a job description and upload your Word resume (`.docx`). The agent autonomously:

1. **Scores your match** — calculates a 0–100% compatibility score with a plain-English summary
2. **Maps your skills** — shows which of your skills align with the role, and which gaps to address
3. **Rewrites your resume bullets** — tailors your existing experience to the specific job posting
4. **Drafts a cover letter** — generates a 3-paragraph cover letter personalized to the role

## Tech stack

| Layer | Technology |
|---|---|
| AI engine | [Anthropic Claude API](https://www.anthropic.com) (`claude-sonnet-4`) |
| Resume parsing | [Mammoth.js](https://github.com/mwilliamson/mammoth.js) — extracts text from `.docx` files in the browser |
| Frontend | Vanilla HTML, CSS, JavaScript — no frameworks, no build step |
| Hosting | GitHub Pages |

## How it works

```
User uploads .docx resume
        ↓
Mammoth.js extracts plain text client-side
        ↓
Job description + resume text → Claude API
        ↓
Claude returns structured JSON (score, skills, bullets, cover letter)
        ↓
Results rendered in the UI
```

The entire pipeline runs in the browser. No backend, no server, no data storage — your resume never leaves your device except for the API call to Anthropic.

## Running locally

No build step needed. Just open `index.html` in a browser — or serve it with any static file server:

```bash
# Option 1: Python
python -m http.server 8000

# Option 2: Node
npx serve .
```

You'll need an [Anthropic API key](https://console.anthropic.com/settings/keys). Enter it in the app — it is used only for the API call and is never stored.

## Deploying to GitHub Pages

1. Fork or clone this repo
2. Go to **Settings → Pages**
3. Set source to **Deploy from a branch → main → / (root)**
4. Your site will be live at `https://YOUR-USERNAME.github.io/job-application-agent`

---

Built by [Your Name](https://github.com/YOUR-USERNAME)
