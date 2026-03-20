# AI Resume Screener

An AI-powered resume screening tool built with vanilla HTML/CSS/JavaScript and the Anthropic Claude API. Paste a job description and up to 10 candidate resumes — Claude ranks, scores, and summarizes every candidate in seconds.

Built as part of an **AI Automation Intern Assessment**.

---

## Demo

> Paste a JD → Add resumes → Click **Screen Candidates with AI** → Get ranked results instantly.

**Sample output:**

| Candidate | Score | Recommendation |
|-----------|-------|----------------|
| Priya Nair | 88 | Strong Fit |
| Alice Wang | 85 | Strong Fit |
| Ben Okafor | 70 | Moderate Fit |
| David Kim | 52 | Moderate Fit |
| Chloe Martinez | 38 | Not Fit |

---

## Features

- **Match score** (0–100) with a visual progress bar
- **Candidate ranking** sorted by fit score
- **Key strengths** (2–3 per candidate)
- **Key gaps** (2–3 per candidate)
- **Fit recommendation**: Strong Fit / Moderate Fit / Not Fit
- **One-line summary** per candidate
- Supports up to **10 resumes** per run
- Built-in **sample data** (1 JD + 5 resumes) to try instantly
- No backend, no database — runs entirely in the browser

---

## How It Works

1. User inputs a **Job Description** and up to 10 **candidate resumes** (plain text)
2. All inputs are bundled into a structured prompt sent to the **Anthropic Claude API**
3. Claude acts as a technical recruiter and returns a ranked **JSON array** with scores, strengths, gaps, and recommendations
4. The UI parses the response and renders each candidate as a scored card

```
[JD + Resumes] → Claude API (claude-sonnet-4) → JSON → Ranked UI Cards
```

---

## Tech Stack

| Layer | Tool |
|-------|------|
| Frontend | HTML, CSS, JavaScript (vanilla) |
| AI Model | Anthropic Claude API (`claude-sonnet-4-20250514`) |
| Hosting | Runs natively inside [Claude.ai](https://claude.ai) as an artifact |

No frameworks. No build step. No backend.

---

## Getting Started

### Option A — Run inside Claude.ai (easiest)

1. Open [Claude.ai](https://claude.ai)
2. Paste the full HTML source from `index.html` into a message and ask Claude to render it as an artifact
3. The Anthropic API key is handled automatically by Claude.ai — no setup needed

### Option B — Run locally with your own API key

> ⚠️ This requires injecting your own Anthropic API key into the fetch call.

1. Clone the repo:
   ```bash
   git clone https://github.com/YOUR_USERNAME/ai-resume-screener.git
   cd ai-resume-screener
   ```

2. Open `index.html` and find the fetch call:
   ```javascript
   const resp = await fetch('https://api.anthropic.com/v1/messages', {
     method: 'POST',
     headers: {
       'Content-Type': 'application/json',
       'x-api-key': 'YOUR_API_KEY_HERE',        // ← add this line
       'anthropic-version': '2023-06-01'         // ← add this line
     },
     ...
   ```

3. Open `index.html` directly in your browser — no server needed.

> Get an API key at [console.anthropic.com](https://console.anthropic.com)

---

## Project Structure

```
ai-resume-screener/
├── index.html       # Complete single-file app (HTML + CSS + JS)
└── README.md        # This file
```

---

## Prompt Design

The core prompt instructs Claude to act as an expert technical recruiter and return only a valid JSON array — no preamble, no markdown fences. Each object in the array contains:

```json
{
  "name": "Alice Wang",
  "score": 85,
  "strengths": ["Strong SQL skills", "Tableau dashboard experience", "A/B testing expertise"],
  "gaps": ["No Python data science experience mentioned", "Limited leadership examples"],
  "recommendation": "Strong Fit",
  "summary": "Highly experienced analyst with a strong match across all core JD requirements."
}
```

Results are sorted by score descending before rendering.

---

## Assessment Context

- **Problem chosen:** Problem 1 — AI Resume Screening System
- **Approach:** Single-page app powered by Claude API. All processing happens client-side via a direct API call. No backend, no database. Inputs are the JD and resume text; output is a ranked JSON array rendered as UI cards.
- **Tools used:** HTML/CSS/JavaScript, Anthropic Claude API
- **Effort:** ~3 hours

---

## License

MIT — free to use, modify, and distribute.
