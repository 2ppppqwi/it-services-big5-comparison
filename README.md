# IT Services Big-5 Competitor Analysis (Generative AI Project)

> A small portfolio project that uses generative AI as a structured analyst — not a summarizer — to produce a side-by-side comparison of five Korean IT-services companies on strategy, investment, ESG, risk, and financials.

[한국어 README →](./README.ko.md)

---

## Why this project

POSCO DX competes in the Korean IT-services market, but most public analyses either profile the company alone or compare it only with the market leader (Samsung SDS). I wanted a frame that places POSCO DX inside a **revenue-tier ladder** so its 2030 target (KRW 4 trillion) can be read as a position, not just a number.

The project's deeper goal: practice a core management-planning skill — *making different companies comparable on the same axes*.

## What's inside

| File | Purpose |
|---|---|
| [`prompt_iteration.md`](./prompt_iteration.md) | Prompt engineering log, v1 → v2 → v3, with the rules added at each step |
| [`build_xlsx.py`](./build_xlsx.py) | Python (openpyxl) script that produces the comparison workbook |
| [`competitor_analysis.xlsx`](./competitor_analysis.xlsx) | 3 sheets: comparison matrix, financial summary with formulas, insights & sources |
| [`competitor_analysis_long.csv`](./competitor_analysis_long.csv) | Long-format CSV (48 rows) for Tableau / BI tools |
| [`metrics.md`](./metrics.md) | Time saved, iterations, matrix size, and two strategic insights |
| [`build_pdf.py`](./build_pdf.py) | ReportLab script that generates a 2-page portfolio with Korean CID fonts |
| [`portfolio.pdf`](./portfolio.pdf) | The 2-page portfolio output |

## Companies covered

A revenue-tier ladder of five companies POSCO DX competes against externally:

1. **Samsung SDS** — KRW 13.8 T
2. **LG CNS** — KRW 6.0 T
3. **Hyundai AutoEver** — KRW 4.3 T
4. **SK AX** (formerly SK C&C) — KRW 2.6 T
5. **Lotte Innovate** — KRW 1.1 T

## Headline results

- **Time:** ~6–8 manual hours → **70 minutes** with AI (≈82% reduction)
- **Iterations:** 3 prompt revisions (v1 → v2 → v3)
- **Matrix:** 5 companies × 12 indicators = **60 cells**
- **Key insight:** POSCO DX's 2030 target (KRW 4 T) lands between Hyundai AutoEver and SK AX — both of which run a *"vertical-domain × AI"* playbook. This re-frames the right competitive reference set away from Samsung SDS.

## The prompt rules that made the output trustworthy

Three rules introduced in v3 of the prompt (see `prompt_iteration.md`):

1. **Quote numbers verbatim from primary sources.** No rounding. Cite document and page where possible.
2. **Unify units to "억원" (KRW 100M)** with YoY % in parentheses.
3. **Never estimate.** If a value isn't disclosed, write `공시 확인 필요` ("disclosure check required") and leave the cell empty.

Rule 3 is what made the deliverable defensible — for example, Lotte Innovate's operating profit was left blank rather than guessed.

## Reproducing the workbook locally

```bash
# Python 3.10+
pip install openpyxl reportlab

python build_xlsx.py     # → competitor_analysis.xlsx + competitor_analysis_long.csv
python build_pdf.py      # → portfolio.pdf
```

## Tech notes

- **openpyxl** for Excel; the operating-margin column uses cell formulas, not pre-computed values, so the workbook recalculates correctly when opened.
- **ReportLab** with built-in CJK fonts (`HYSMyeongJo-Medium`, `HYGothic-Medium`) — no external font files required for Korean rendering.
- **Long-format CSV** is intentional: human-readable comparison goes in Excel; Tableau/BI tools work best with one row per (company, axis, value).

## What I'd do next with more time

- Add 3-year time series for revenue / operating profit so the ladder shows direction, not just position.
- Pull ESG controversies from MSCI/Sustainalytics to balance the self-reported ESG narrative.
- Add a sixth company (Naver Cloud or Kakao Enterprise) to test whether the "vertical-domain × AI" pattern holds outside SI-rooted players.

## License

MIT (see `LICENSE`).

## Author

Jimin Song · jimin.song616@gmail.com
