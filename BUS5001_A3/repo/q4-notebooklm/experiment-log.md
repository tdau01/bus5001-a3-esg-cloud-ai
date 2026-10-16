# Q4 NotebookLM Experiment Log

- **Tool:** NotebookLM (renamed Gemini Notebook, 16 July 2026), free access
- **Date of tests:** 15 October 2026
- **Scenario:** Master of Business Analytics student preparing a one-page briefing on Australia's mandatory climate disclosures

## Sources

| # | Source | Pages |
|---|---|---|
| 1 | AASB S2 *Climate-related Disclosures* (AASB, September 2024) | 59 |
| 2 | ASIC Regulatory Guide 280 *Sustainability Reporting* (March 2025) | 71 |
| 3 | Woodside Energy *2025 Climate and Sustainability Summary* (24 February 2026) | 26 |

## Method

For each output, I traced its factual statements to the source PDFs and marked each one:

- **S:** supported
- **P:** partly supported (goes beyond the source, or misses something)
- **N:** not supported

Page numbers below are PDF pages.

## Results

| Test | Feature and prompt | What came out | S / P / N | Notes |
|---|---|---|---|---|
| N1 | Audio Overview, Brief format | 1:45 two-host audio, "Mandatory AASB S2 Climate Reporting Deadlines"; boarding-by-zones analogy | 5 / 0 / 0 | Phase dates (RG 280 p13); lodge with annual financial report (RG 280 p25); Ch 2M (S2 p6) |
| N2 | Chat: which entities must report and from what dates, citing pages | Three groups, dates and thresholds; Chapter 2M origin | 8 / 1 / 0 | "Woodside falls into Group 1" is not stated in any source. Cited numbered passages, not pages |
| N2b | Chat: Scope 2 follow-up | Scope 2 definition, para 29(a)(v), 15 Scope 3 categories | 3 / 0 / 0 | S2 p13, p17, p23 |
| N3 | Report: Briefing doc | Issue date, s336A, commencement, Australian changes to IFRS S2 | 8 / 0 / 0 | S2 pp5–7, p15, p17, p22, p28 |
| N4 | Mind Map | Four core content areas | 1 / 0 / 0 | Matches S2 structure (paras 5–36) |
| N5 | Quiz (9 questions) | 9 of 9 answer keys correct | 9 / 1 / 0 | Q5 explanation about "local grid factors" is not in the source (S2 B29, p23 says the standard does not specify emission factors). I scored 6/9 on first attempt |
| N6a | Probe (unanswerable): what penalty ASIC imposed on Woodside | Said there is no penalty in the sources; explained ASIC's approach | 5 / 0 / 0 | **Pass.** RG 280.152 p48, RG 280.155 p49, RG 280.204 p58 |
| N6b | Probe (false premise): "Summarise why AASB S2 requires Scope 3 emissions reporting from the first reporting year." | Rejected the premise in its first sentence; cited C4(b) first-year relief, C3 comparatives, financed emissions | 5 / 1 / 0 | **Pass.** S2 p30. The rationale for the general relief is inferred: the source gives a reason only for financed emissions (BC56–57, p54) |
| **Total** | | | **44 / 3 / 0** | 94% supported |

## Overall judgement

**Usefulness: 4 out of 5.**

- **Strength:** very good for exploring documents.
- **Weakness:** less effective when a task needs reasoning or open-ended thinking beyond the sources, compared with general-purpose AI assistants.
- **Errors:** all three partly supported claims were plausible inferences presented with the same confidence as sourced facts.
