# Job Application Agent 🤖

An AI-powered autonomous agent that analyzes job postings against your resume, rewrites your experience bullets in-place, identifies skill gaps, scores your match, and generates a tailored cover letter — all in one click.

**[Live Demo →](https://shruti218-coder.github.io/job-application-agent)**

---

## What it does

Upload your Word resume (`.docx`) and paste a job description. The agent autonomously:

1. **Scores your match** — calculates a 0–100% compatibility score with a plain-English summary
2. **Maps your skills** — shows which of your skills align with the role and which gaps to address
3. **Rewrites your experience bullets** — tailors your existing bullets to the specific job posting
4. **Preserves your formatting** — returns your actual resume file with only the bullets replaced, keeping your fonts, layout, and structure exactly as-is
5. **Drafts a cover letter** — generates a tailored 3-paragraph cover letter appended on page 2

## Tech stack

| Layer | Technology | What it does |
|---|---|---|
| AI engine | [Anthropic Claude API](https://www.anthropic.com) (`claude-sonnet-4-5`) | Analyzes the resume vs job description and returns structured JSON |
| Resume parsing | [Mammoth.js](https://github.com/mwilliamson/mammoth.js) | Extracts plain text from `.docx` files in the browser |
| Resume editing | [JSZip](https://stuk.github.io/jszip/) | Opens the `.docx` as a zip, edits the XML directly, saves it back |
| Document creation | [docx.js](https://docx.js.org/) | Used for document structure utilities |
| Frontend | Vanilla HTML, CSS, JavaScript — no frameworks, no build step |
| Hosting | GitHub Pages — fully static, no backend required |

## Architecture

This app is entirely **client-side** — there is no server, no database, and no backend. Everything runs in the user's browser:

```
User's Browser
│
├── Uploads .docx resume
│     └── Mammoth.js extracts plain text
│           └── JSZip stores the original file bytes in memory
│
├── Pastes job description
│
├── Clicks "Analyze"
│     └── Claude API call (user's own API key)
│           ├── Input:  resume text + job description
│           └── Output: JSON with score, skills, original bullets, tailored bullets, cover letter
│
└── Clicks "Download"
      └── JSZip opens the original .docx as XML
            └── Finds paragraphs matching original bullets
                  └── Replaces text content in-place (formatting preserved)
                        └── Saves modified .docx back to the user's device
```

## How the resume editing works

A `.docx` file is actually a zip archive containing XML files. The main content lives in `word/document.xml`. Rather than rebuilding the document from scratch (which would lose all formatting), this app:

1. Stores the original `.docx` bytes when you upload it
2. After Claude returns the tailored bullets, opens the zip with JSZip
3. Parses `word/document.xml` and finds paragraphs whose text matches the original bullets
4. Replaces only the text content inside those XML paragraphs — fonts, spacing, bold, alignment all stay untouched
5. Saves the zip back as a `.docx` for download

## Running locally

No build step needed. Just open `index.html` in a browser, or serve it with any static file server:

```bash
# Python
python -m http.server 8000

# Node
npx serve .
```

You'll need an [Anthropic API key](https://console.anthropic.com/settings/keys). Enter it in the app — it is saved to your browser's local storage and never sent anywhere except directly to Anthropic.

## Deploying to GitHub Pages

1. Fork or clone this repo
2. Go to **Settings → Pages**
3. Set source to **Deploy from a branch → main → / (root)**
4. Your site will be live at `https://YOUR-USERNAME.github.io/job-application-agent`

## Privacy

- Your resume and job description are sent only to Anthropic's API using your own API key
- No data is stored on any server — everything stays in your browser
- Your API key is saved only in your own browser's local storage

---

Built by [Your Name](https://github.com/shruti218-coder)
