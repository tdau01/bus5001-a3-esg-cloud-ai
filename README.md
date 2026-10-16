# ESG Cloud AI Evaluation: GreenDesk Chatbot, LLM Triage and NotebookLM

Evidence repository for a consulting report on how cloud-enabled AI can support an organisation's sustainability operations and ESG reporting. The repository holds the build files, raw outputs, test logs and screenshots behind the results in the report.

---

## Repository structure

```
├── README.md
├── q1-dialogflow/          GreenDesk ESG Assistant (Dialogflow CX)
│   ├── export/             Agent export file
│   ├── screenshots/        Figures 1–9, B1–B3, Transcripts 1–2
│   ├── transcripts/        T01 and T02 conversation text
│   └── test-log.md         Test cases T01–T12 and results
├── q3-llm-triage/          LLM message triage (Gemini vs baselines)
│   ├── Q3_ESG_LLM_Triage.ipynb
│   ├── prompts/            Original and revised prompt
│   ├── results/            Raw outputs, baselines, consistency and accuracy files
│   └── screenshots/        Figures 11–15, Listing 1, Appendix C outputs, Figure C1
├── q4-notebooklm/          NotebookLM (Gemini Notebook) evaluation
│   ├── experiment-log.md   Tests N1–N6b with claim checks
│   ├── sources.md          The three source documents and links
│   ├── screenshots/        Figures 16–20, E1–E5
│   └── audio/              Audio Overview (optional)

```

---

## Q1: GreenDesk ESG Assistant (Dialogflow CX)

A sustainability incident reporting assistant. Staff report an ESG issue (energy or water waste, waste and recycling, hazardous materials, accessibility barriers, health and safety); the bot collects the issue type, location and severity, confirms a summary, and either logs the report for the right team or escalates critical and hazardous cases to a person.

| Item | Detail |
|---|---|
| Platform | Dialogflow CX (Conversational Agents console), Flow agent |
| Region / language | australia-southeast1 / English |
| Intents | 6 (Default Welcome Intent, report.start, report.confirm, report.change, report.cancel, human.agent) |
| Entities | @issue_type (custom), @severity (custom), location as @sys.any |
| Pages | Start Page, Report Details (form), Review Report, Logged, Escalate, Cancelled |
| Escalation | Critical severity, hazardous issues, a request for a person, or three consecutive unrecognised inputs |
| Testing | Saved test cases, all passing on the final run (see `test-log.md`) |

**Files**
- `export/`: agent export; can be restored in a new Dialogflow CX agent via Agent settings > Restore.
- `test-log.md`: every test, the input sequence, the result and any fix applied.
- `transcripts/`: two example conversations (standard logged path and escalation path).
- `screenshots/`: flow, intents, entity, form parameters, routes, no-match handlers and test results.

---

## Q3: LLM triage of ESG messages

Ten employee messages (five sample messages, three edge cases, two held-out paraphrases) were classified by Gemini using an original and a revised prompt, then compared with a keyword-rule baseline and a Hugging Face zero-shot classifier against manually assigned gold labels.

| Setting | Value |
|---|---|
| Run date | 15 October 2026 |
| Model | gemini-3.6-flash, with automatic fallback to gemini-3.5-flash-lite during 503 "high demand" errors (fallback use is recorded in the report) |
| Temperature | 0 |
| Runs | Original prompt × 1, revised prompt × 3 |
| Baselines | Keyword rules; facebook/bart-large-mnli zero-shot |

**Headline results (revised prompt, run 1)**

| Method | Category | Urgency | Follow-up | Team |
|---|---|---|---|---|
| Gemini, revised prompt | 0.8 | 0.7 | 1.0 | 0.6 |
| Keyword rules | 0.8 | 0.7 | 0.9 | 0.8 |
| Zero-shot (bart-large-mnli) | 0.5 | 0.2 | 0.7 | 0.6 |

**Files in `results/`**

| File | Contents |
|---|---|
| `run_log.md` | Date, model, temperature and run settings |
| `gold_labels.csv` | Manually assigned correct labels for the 10 messages |
| `original_prompt_outputs.jsonl` | Raw answers from the original prompt |
| `revised_prompt_outputs.jsonl` | Raw JSON answers from the revised prompt, 3 runs |
| `revised_prompt_runs.csv` | Parsed fields per run and message |
| `llm_consistency_by_message.csv` | Whether each field was identical across the 3 runs |
| `baseline_rules.csv` | Keyword-rule baseline output |
| `baseline_zero_shot.csv` | Zero-shot classifier output and scores |
| `comparison_table.csv` | Gold labels side by side with all three methods |
| `accuracy_vs_gold.csv` | Accuracy per method and field |

**Reproducing the run**
1. Open `Q3_ESG_LLM_Triage.ipynb` in Google Colab.
2. Run the cells in order. When the API key prompt appears, paste your own Gemini API key (from Google AI Studio). The key is entered at run time and is never saved in the notebook.
3. The final cell saves all result files to `results/` and downloads them as a zip.

Results may differ slightly on a new run because hosted models are updated over time.

---

## Q4: NotebookLM (Gemini Notebook) evaluation

NotebookLM was tested on 15 October 2026 for an academic scenario: preparing a briefing on Australia's mandatory climate disclosures. The notebook used three public sources (AASB S2, ASIC Regulatory Guide 280 and Woodside Energy's 2025 Climate and Sustainability Summary; see `sources.md`).

| Feature tested | Claims checked | Supported | Partly | Not supported |
|---|---|---|---|---|
| Chat with sources (two questions) | 12 | 11 | 1 | 0 |
| Briefing document | 8 | 8 | 0 | 0 |
| Audio Overview | 5 | 5 | 0 | 0 |
| Mind Map | 1 | 1 | 0 | 0 |
| Quiz (9 questions) | 10 | 9 | 1 | 0 |
| Probe 1: unanswerable question | 5 | 5 | 0 | 0 |
| Probe 2: false premise | 6 | 5 | 1 | 0 |
| **Total** | **47** | **44 (94%)** | **3** | **0** |

Every claim was traced to a page in the source PDFs; the full log with page references is in `experiment-log.md`. The source PDFs are linked, not stored, to respect the publishers' copyright.

---

## Notes

- No API keys, passwords or personal data are stored in this repository.
- Names in test messages are fictional.
- Figure numbers in file names match the figure numbers in the report.
