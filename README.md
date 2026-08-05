# JobFair AI

**Detecting Inflated Skill Requirements in Indian Tech Job Postings using SQL, Python & Generative AI**

Submitted for the Imarticus Learning Data Science Project Competition — July 2026 Edition.

## Problem Statement

Job postings in the Indian tech industry often list inflated requirements — asking for years of experience and long skill lists for what are essentially entry-level roles. This causes qualified candidates, especially freshers, to self-reject from roles they could actually perform, while recruiters sift through mismatched applications.

## Overall Solution Approach

A four-stage pipeline:

1. **Clean & Structure** — ~19,600 real job postings (Naukri.com) cleaned in Python; regex-based skill extraction and experience parsing
2. **MySQL Database** — Normalized `postings` and `skills` tables (one-to-many relationship) enabling real SQL joins and aggregations
3. **SQL Analysis** — Baseline skill demand calculated per seniority band, most in-demand skills identified, worst-offender companies flagged
4. **GenAI Chatbot** — An inflation score is computed in Python for every posting; a live chatbot (Llama 3.1 via the Groq API) explains the result in plain language, grounded entirely in the real computed data (retrieval before generation)

## Key Findings

| Seniority Band | Avg. Skills Required | # Postings |
|---|---|---|
| Entry Level (0–2 yrs) | 6.50 | 7,417 |
| Mid Level (3–6 yrs) | 6.48 | 9,225 |
| Senior Level (7+ yrs) | 6.49 | 2,593 |

- **28.8% of postings** (nearly 1 in 3) were flagged as demanding meaningfully more skills than typical for their experience level
- Skill demand barely changes across seniority bands — entry-level candidates are expected to show almost the same skill breadth as 7+ year veterans
- **Times Internet** topped the list of entry-level postings with the highest average skill demand (8.33 skills)

## Further Improvement Areas / Next Steps

- Validate baselines against real hiring outcome data, not just posting text
- Expand the chatbot to compare against live/current market postings instead of a static dataset
- Package as a browser extension for direct use on Naukri / LinkedIn
- Standardize skill names (case and synonym matching) for cleaner aggregation

## Justification of the Overall Project

This project addresses a real, shared cost in the hiring market:

- **For candidates** — reduces false self-rejection caused by postings that look scarier than the role actually is
- **For recruiters** — signals where their own postings may be filtering out good candidates for the wrong reasons

## Tech Stack

Python (pandas, re) · MySQL · SQL (joins, aggregations, CASE statements) · Groq API (Llama 3.1-8B-Instant)

## Repository Structure

```
jobfair-ai/
├── README.md
├── notebook/
│   └── JobFair_AI_Analysis.ipynb
├── data/
│   └── naukri_job_postings.csv
├── presentation/
│   └── JobFair_AI_Presentation.pptx
└── requirements.txt
```

## Running This Project

1. Install dependencies: `pip install -r requirements.txt`
2. Set up a local MySQL database and update the connection string in the notebook
3. Get a free API key from [Groq Console](https://console.groq.com) and set it as an environment variable:
   ```bash
   export GROQ_API_KEY="your_key_here"
   ```
4. Run the notebook cells in order


Yash Govalkar —  Imarticus Learning, Mumbai

